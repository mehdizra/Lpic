---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[207.1 Basic DNS server configuration]]"
date: 2023-10-13
---
## named.conf
فایل اصلی تنظیمات سرور دومین ما همین فایل است و میتوانیم با دستور تنظیمات مختلفی را به آن تزریق کنیم
```
// This is the primary configuration file for the BIND DNS server named.
//
// Please read /usr/share/doc/bind9/README.Debian.gz for information on the
// structure of BIND configuration files in Debian, *BEFORE* you customize
// this configuration file.
//
// If you are just adding zones, please do that in /etc/bind/named.conf.local

include "/etc/bind/named.conf.options"; # آپشن های سرور
include "/etc/bind/named.conf.local"; # زونهایی که در سرور وجود دارند
include "/etc/bind/named.conf.default-zones"; سوال؟
include "/etc/bind/keys/test.key" آدرس فایل قفل ارتباط سرورهای مستر و اسلیو
~                                                                             ~                                  
```
#### [[TSIG]] key configuration 
```
include "/etc/bind/named.conf.options";
include "/etc/bind/named.conf.local";
include "/etc/bind/named.conf.default-zones";
key "foo" {
        algorithm hmac-sha256;
        secret "PN9fhYSilZ8A4N0QCUa2WUuA5lPVKDDQ5d0j0J2X9MQ=";
};
```

میتوانیم کلید را در فایل دیگری ذخیره کنیم و اینکلود کنیم
```
include "/etc/bind/named.conf.options";
include "/etc/bind/named.conf.local";
include "/etc/bind/named.conf.default-zones";
include "/etc/bind/keys/foo.key" 
```

برای سرور مستر در تنظیمات کانف.لوکال این خط را اضافه میکنیم
[[named.conf#named.conf.local]]
```
 alow-transfer { key foo; };
```

برای تنظیم سرور اسلیو در تنظیمات آپشن این خطوط را اضافه میکنیم
[[named.conf#named.conf.options]]
```
server 1.2.3.4 { # آدرس سرور مستر
	transfer-format many-answers;
	keys {foo }; 
};
```
### named.conf.local
در این فایل زون هایمان را تعریف میکنیم و آدرس آنها را برای سرور مشخص میکنیم
طبق همان آدرسی که مشخص کردیم باید فایل کانفیگوریشن زون وجود داشته باشد.
```bash
root@mvm:/etc/bind# vim named.conf.local
# clear comment
zone "foo.gandotech.com." {
        type master;
        file "/etc/bind/zones/foo.gandotech.com.conf;
}
# save and exit
```
#### Master & Slave
اگر سروری که ایجاد میکنیم اسلیو باشد و تنظیمات خود را از سرور مستر دیگری بگیرد تنظیمات در دو فایل لوکال سرور مستر و سرور اسلیو به این شکل خواهد بود:
##### تنظیمات مستر
```bash
root@mvm:/etc/bind# vim named.conf.local
# clear comment
zone "foo.gandotech.com." {
        type master;
        file "/etc/bind/zones/foo.gandotech.com.conf;
        notify yes;
        also-notify { 4.3.2.1; }; # آدرس سرور اسلیو
        alow-transfer { 4.3.2.1; }; # آدرس هایی که مجاز به ارتباط با ما هستن 
}
# save and exit
```
##### تنظیمات اسلیو
```bash
root@mvm:/etc/bind# vim named.conf.local
# clear comment
zone "foo.gandotech.com." {
        type slave;
        file "/etc/bind/zones/foo.gandotech.com.conf;
        masters { 1.2.3.4; }; # آدرس مستر یا مسترهایی که قرار است آبدیت ها را از آنها بگیریم
}
# save and exit
```

### create zone file
برای زون جدیدی که میخواهیم داشته باشیم یک فایل کانفیگ در فولدر زون طبق آدرسی که در فایل بالا قرار دادیم، ایجاد میکنیم
```shell
root@mvm:/etc/bind# mkdir zones
root@mvm:/etc/bind# touch zones/foo.gandotech.com.conf
```

در این مثال آدرسی که برای آن فایل ایجاد کردیم زون اوریجین ما هست و با ات ساین نمایش داده میشود.
@ به جای foo.gandotech.com.
نقطه آخر در تنظیمات کانفیگ مهم است.
```shell
root@mvm:/etc/bind# vim zones/foo.gandotech.com.conf
$TTL 300
@ IN SOA ns.foo.gandotech.com. akbar.gmail.com (
        1; Serial
        1; Refresh
        1; Retry
        1; Expire
        300; Negative TTL
)
@ NS ns1
@ NS ns2

ns1 A 1.2.3.4
ns2 A 1.2.3.5
ns3 CNAME ns2
esx A 1.1.1.1
firewall A 2.2.2.2
www.shiraz A 3.3.3.3
```
در مثال بالا نیم سرور ما ان اس 1 و 2 هستند.
و آی پی این دو سرور 1.2.3.4 و 1.2.3.5 هستند.
سرویس های دیگری هم روی این سرور تعریف شده اند.
سرور ان اس 3 از ان اس 2 فراخوانی می شود.
میتوانیم با این دستور از خودمان کوئری بگیریم.
اما قبلش باید سرویس بایند را ریستارت کنیم.
```shell
 mehdi@mvm:~$ systemctl restart bind9
 mehdi@mvm:~$ dig A ns1.foo.gandotech.com @127.0.0.1
```

در ادامه میخواهیم میل سرور اضافه کنیم و فایل کانفیگ رو مرتب کنیم
برای مرتب سازی رکورد ها را برمبنای تایپ آنها زیر هم قرار میدهیم.
```shell
root@mvm:/etc/bind# vim zones/foo.gandotech.com.conf
$TTL 300

@ IN SOA ns.foo.gandotech.com. akbar.gmail.com (
        1; Serial
        1; Refresh
        1; Retry
        1; Expire
        300; Negative TTL
)
@ NS ns1
@ NS ns2

@ MX 10 mail17.mailchimp.com.
@ MX 20 mail18.mailchimp.com.
shiraz MX 10 mail.shiraz

ns1 A 1.2.3.4
ns2 A 1.2.3.5
esx A 1.1.1.1
firewall A 2.2.2.2
www.shiraz A 3.3.3.3
mail.shiraz A 5.5.5.5

ns3 CNAME ns2
```
در این سناریو ما برای سرویس میل فو از سرویس خارجی میل چیمپ استفاده کردیم.
برای سرویس میل شیراز دات فو از سرویس داخلی استفاده کردیم و یک آی پی هم برای آن در نظر گرفتیم.
### named.conf.options
این فایل در همان فولدر بایند قرار دارد و برای تنظیمات بایند استفاده می شود.
در این مثال ما میخواهیم تنظیمات امنیتی سرور را انجام دهیم.
```
listen-on-v6 {any;}; # باز بودن تمامی آی‌پی های ورژن6 ورودی
listen-on {any;}; # default باز بودن تمامی آی‌پی های معمولی ورودی
listen-on {192.168.59.1;} باز بودن یک کارت شبکه خاص برای رکوئست های ورودی
allow-query {any;}; # default در صورتی که سرور ما به عنوان سرور وب سایت تعریف شده باید امکان رکوئست گرفتن از تمامی سرورهای دنیا را داشته باشد.
allow-query {127.0.0.0/8; 192.168.59.0/24;} # نمونه ای از تنظیم سرور برای شبکه های لوکال
recursion no; #امکان کشینگ سرور برای رکوئست های خارجی خاموش است
recursion yes; # (default)امکان کشینگ سرور برای رکوئست های خارجی روشن است
allow-recursion {127.0.0.0/8; 192.168.59.0/24;}; # با این تنظیم رکوئست برای جستجوی هاست های خارج از سازمان برای افراد داخل سازمان باز می شود.
```

