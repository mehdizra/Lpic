---
tags:
  - "#webservice"
  - HTTP
  - Apache
up: "[[LPIC2 Sessions map of content]]"
date: 2023-10-17
---
### web server
امروزه خیلی از اپلیکیشن ها با متد زیر طراحی می شوند.
در این متد هسته نرم افزار در بکند قرار دارد و با دیتابیس ارتباط دارد.
در لایه بالاتر یک وب سرور است که با API با بکند در ارتباط است.
وب سرور با تمامی پلتفورم ها در قالب HTTP (Hypertext transfer protocol) در ارتباط است. و هر پلتفورم کلاینت یک برنامه ای است که صرفا اطلاعاتی را که از وب سرور خود دریافت کرده به کاربر نمایش میدهد و از کاربر اطلاعات جدید را دریافت کرده و به وب سرور خود ارسال میکند.
وب سرورهای مختلفی وجود دارد مثل Apache, Nginx, IIS که ما در این دوره با Apache کار میکنیم.
![[Pasted image 20231030115610.png]]

### پروتکل HTTP
- یک پروتکل لایه هفتی است. در این پروتکل تمامی request , response ها به صورت متنی است.
- این پروتکل یک پروتکل stateless است بر خلاف موارد stateful 
- یعنی هر رکوئست یا ریسپانس به صورت مجزاست و حاوی حافظه یا ارتباط با رکوئست، ریسپانس های دیگر نیست.
- بنابراین برای مثال جهت لاگین بودن در وب سایتها از مکانیزمهای مختلفی مثل کوکی ها استفاده می شود.
- مثلا وقتی با یک browser در یک وب سایت لاگین میکنیم، یک session id رندوم ایجاد میشود و در response بعدی به سرور ارسال می شود. سرور از طریق این کوکی متوجه می شود که ما در آن وب سایت لاگین شده ایم یا خیر و چه ویژگی هایی به عنوان کاربر داریم.
#### HTTP client 
ما کلاینت های HTTP زیادی داریم. پرکاربردترین کلاینت Browser ها هستند.
از دیگر کلاینت ها میتوان به این موارد اشاره کرد:
کامند curl
کامند wget
نرم افزار postman
انواع ماژول request در زبان های برنامه نویسی
نرم افزارهای تحت وب در موبایل‌ها کامپیوترها
> [!idea] گسترده ترین پروتکل در دنیا HTTP است. بنابراین در تمامی زبان های برنامه نویسی و سیستم عامل ها انواع کلاینت های HTTP وجود دارد.

**این که بروزرها میتوانند انواع سایتهای مختلف را در ظاهر های متفاوت به ما نشان دهند ارتباطی به خود پروتکل http ندارد. در واقع ریکوئست، ریسپانسهای http میتواند حاوی content باشد که این content قالب های مختلفی مثل صدا، تصویر یا متن html باشد. یکی از وظایف browser این است که متن های html را اصطلاحا pars کند و به صفحات وب تبدیل کند**

![[Pasted image 20231030122302.png]]
- یک آدرس URL شامل چند بخش است: پروتکل، هاست، پت
- موارد دیگری مثل پورت یا کوئری هم میتواند در این آدرس گنجانده شود.
- یک http کلاینت این آدرس را تبدیل به رکوئستی میکند که برای سرور قابل فهم است.
- متدهای مختلفی برای رکوئست های http داریم مثل: get, post, head, put, connect, del
- متدپیش فرض معمولا get است.
- متدها multiline هستند و هر خط با یک CRLF (carriage return, line feed) یا همان ==\r\n== به پایان میرسد.
- دو CRLF پشت سر هم به معنای پایان رکئوست است.
![[Pasted image 20231030123956.png]]
#### http request
رکوئست به شکل زیر ارسال می شود:
- نوع رکوئست مثلا get فاصله path فاصله ورژن http پایان خط یا همان CRLF
- نام هدر دو نقطه مقدار هدر و یک CRLF به ازای هر هدر
- پس از آخرین هدر که خود حاوی یک CRLF است یک CRLF دیگر به معنای پایان رکوئست است.

> [!idea] زمانی که بخواهیم یک رکوئست لایه هفت به صورت basic به یک سرویس دهنده استفاده کنیم میتوانیم از دستور [[netcat]] استفاده کنیم.
> نت کت ابزار بسیار قدرتمندی است. میتواند هم سرور و هم کلاینت در udp و tcp شود
> میتوانیم ارتباط بین دو سرور را از طریق nc چک کنیم.

#### http response
ریسپانس به شکل زیر ارسال می شود:
ورژن http فاصله status code فاصله توضیح status code (که ازین طریق میفهمیم نتیچه رکوئست چی بوده مثلا 200 اوکی هست و 400 به معنای رکوئست اشتباه)
هدر date:
هدر سیگنیچر server:
هدر Content-Length: طول محتوای اتچ شده به بایت
هدر connection: باز یا بسته بودن ارتباط
هدر content-type: نوع محتوا مثل متن یا باینری
بعد از یک خط خالی محتوا شروع می شود.

##### مثال http response
وب سرور ما به صورت پیش فرض روی پورت 80 فعال است. اگر از طریق نت کت یک کلمه بروی این پورت ارسال کنیم نتیجه ریسپانس حاوی bad request  خواهد بود. چون طبق استاندارد http این پیام را ارسال نکردیم.
```BASH
mehdi@mvm:~$ echo "salam" | nc 127.0.0.1 80
HTTP/1.1 400 Bad Request
Date: Mon, 30 Oct 2023 10:10:40 GMT
Server: Apache/2.4.52 (Ubuntu)
Content-Length: 301
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>400 Bad Request</title>
</head><body>
<h1>Bad Request</h1>
<p>Your browser sent a request that this server could not understand.<br />
</p>
<hr>
<address>Apache/2.4.52 (Ubuntu) Server at 127.0.1.1 Port 80</address>
</body></html>
```
##### دسته بندی status code ها
- دسته 1X پاسخهای informational
- دسته 2X پاسخهای successful
- دسته 3X پاسخهای redirection
- دسته 4X پاسخهای client errors
- دسته 5X پاسخهای server errors
لیست کامل رو میتوان از سایتهای مختلف پیدا کرد.

##### مثالی برای http request متد get
برای ارسال یک رکوئست کامل به صورت دستی باید از متد GET استفاده کنیم. میتوانیم با استفاده از دستورات [[echo]] , [[netcat]] برای ارسال این متن به سرور مربوطه استفاده کنیم
```bash
mehdi@mvm:~$ echo -ne "GET / HTTP/1.1\r\nHost: 37.228.137.172\r\n\r\n" | nc 37.228.137.172 80
HTTP/1.1 200 OK
Date: Thu, 02 Nov 2023 16:10:39 GMT
Server: Apache/2.4.52 (Ubuntu)
Last-Modified: Tue, 17 Oct 2023 17:19:45 GMT
ETag: "d-607ecbaa9534c"
Accept-Ranges: bytes
Content-Length: 13
Content-Type: text/html

<h1>SALAM</h1>
```
میتوانیم از دستورات [[cat]] , netcat هم استفاده کنیم، البته باید متن رکوئست از قبل در یک فایل ذخیره شده باشد و آن فایل را ارسال کنیم.
```bash
mehdi@mvm:~$ request.txt | nc 37.228.137.172 80
```
> [!idea] به بخش بالایی ریسپانس header و به بخش پایینی آن content میگوییم.
> بنابراین میتوانیم با متد head فقط هدر را در ریسپانس دریافت کنیم.

##### مثالی برای http request متد HEAD
این بار بجای ارسال درخواست ریشه سایت، یک فایل را درخواست میکنیم.
```bash
mehdi@mvm:~$ echo -ne "HEAD /test.jpg HTTP/1.1\r\nHost: 37.228.137.172\r\n\r\n" | nc 37.228.137.172 80
HTTP/1.1 200 OK
```
در صورت وجود چنین فایلی در سرور کد 200 OK
در صورت نبودن چنین فایلی کد 404 Not found
و در صورت نداشتن permission به فایل مورد نظر کد 403 Forbidden دریافت خواهیم کرد.

> [!code] [[curl]] #command
> یک کلاینت http بسیار عالیست و مارا از نوشتن رکوئست بی نیاز میکنه

```bash
mehdi@mvm:~$ curl 37.228.137.172
<h1>SALAM</h1>
```
با استفاده از -v میتوانیم نحوه رکوئست زدن curl را ببینیم:
علامت > رکوئست هاست و علامت < ریسپانسهاست
```bash
mehdi@mvm:~$ curl -v 37.228.137.172
*   Trying 37.228.137.172:80...
* Connected to 37.228.137.172 (37.228.137.172) port 80 (#0)
> GET / HTTP/1.1
> Host: 37.228.137.172
> User-Agent: curl/7.81.0
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Thu, 02 Nov 2023 20:14:25 GMT
< Server: Apache/2.4.52 (Ubuntu)
< Last-Modified: Tue, 17 Oct 2023 17:19:45 GMT
< ETag: "d-607ecbaa9534c"
< Accept-Ranges: bytes
< Content-Length: 13
< Content-Type: text/html
<
<h1>SALAM</h1>
* Connection #0 to host 37.228.137.172 left intact
```

> [!idea] سرور با توجه به ورژن http کلاینت ها میتواند ریسپانس متفاوتی را ارسال کند.
> مثلا هدر accept-encoding میتواند کانتنت را به صورت زیپ شده ارسال و دریافت کند.

با توجه به اینکه رکوئست http در ابزارهای مختلف و زبان های برنامه نویسی مختلف تعریف شده باید در نظر داشته باشیم که از طرق مختلف میتوان به یک وب سایت دسترسی داشت و این موضوع صرفا از طریق وب بروزر اتفاق نمی افتد.

> [!danger] ارسال رکوئست به آدرس یک فولدر معنایی ندارد.
> در صورتی که به یک فولدر رکوئست ارسال شود، سرور به دنبال index.html می گردد و در صورت پیدا نکردن و فعال بودن آپشن Indexing  یک صفحه وب برای نمایش آن فولدر ایجاد می کند، اصطلاحا on the fly generate می کند.

> [!search] در صورت نیاز، تغییر آپشن indexing در سرور Apache2 و تغییر فایل پیش فرض سرور از index.html به فایل دیگر سرچ شود. 

![[Pasted image 20231103182642.png]]
### Apache2
وب سرور apache یکی از معروف ترین سرورهای وب است.
بعد از نصب روی یک ماشین اگر روی ip آدرس اون ماشین یک رکوئست ارسال شود. پیج پیشفرض وب دیده خواهد شد که آدرس آن /var/www/html است.
درواقع default document root سرور apache بر اساس کانفیگوریشن همین است.

کانفیگوریشن فایل اصلی سرویس آپاچی در توزیع های دبین و اوبونتو این فایل است: 
```bash
/etc/apache2/apache2.conf
```
> [!search] در صورت نیاز، تنظیمات سرور apache جستجو شود.

#### نکاتی در مورد تنظیمات سرور apache
کانفیگوریشن های apache تشکیل شده از یک سری directive مثل serverRoot , DefaultRunDir , ...
1. این دایرکتیو ها case sensitive نیستند ولی معمولا به صورت title case نوشته می شود. مثال: MaxKeepAliveRequests 100
2. مقدار هر دایرکتیو با یک اسپیس جدا میشود، اما گاهاً از = هم استفاده می کنیم.
3. یک سری دایرکتیو هستند به نام کانتینر مثل کانتینر <Directory />
4. کانتینر ها با علامات </ > باز و بسته می شود و مقدار آن با فاصله از اسم تعریف می شود. در صورت صحیح بودن مقدار موارد داخل کانتینر اعمال می شود. در واقع مثل if در زبان های برنامه نویسی عمل میکند.
مثال
```bash
<Directory />
        Options FollowSymLinks
        AllowOverride None
        Require all denied
</Directory>

<Directory /usr/share>
        AllowOverride None
        Require all granted
</Directory>
```

 > [!question] چرا در یکی از تنظیمات پیش فرض apache فایل هایی با .ht شروع میشوند در ریسپانسها forbidden می شوند؟
 > چون یک سری از فایل های تنظیمات و پسوردها با این اسم شروع می شود.
 
در تنظیمات apache با define میتوانیم متغیر تعریف کنیم. 
> [!search] در صورت نیاز، تعریف متغیر در apache جستجو شود.

#### دایرکتیو LogFormat
تمامی رکوئست هایی که به سرور ارسال میشود توسط سرور لاگ می شود. فرمت لاگ شدن رکوئست ها اینجا تعریف می شود.
> [!search] در صورت نیاز، LogFormat سرچ شود.
> 

برای دیدن لاگ های apache میتوانیم ازین دستور [[tail]] استفاده کنیم.
```BASH
mehdi@mvm:~$ tail -fn0 /var/log/apache2/access.log
mehdi@mvm:~$ tail -fn0 /var/log/apache2/error.log
```
fn0 باعث میشود لاگ های قبلی رو نبینیم و لاگهای جدید را به صورت لایو ببینیم.

وب سرور ما به چه پورتهایی listen میکند؟
```bash
root@mvm:~# netstat -lnpt | grep apache
tcp6   0   0 :::80     :::*    LISTEN   947/apache2
```
مثال بالا نشان میدهد که روی همه اینترفیسها در پرت 80 اصطلاحا listen میکند.

#### تنظیم پورتها
در فایل apache2.conf دایرکتیوهایی به نام include و IncludeOptional وجود دارند که تنظیمات را از فایلهای دیگر وارد فایل اصلی میکند. (مثل تنظیمات DNS)
در توزیع اوبونتو تنظیمات مربوط به پورتها در فایلی غیر از فایل اصلی است و با دایرکتیو include وارد تنظیمات اصلی شده است.
در include ها مسیرهای رلتیو از سرورروت به بعد است
پیش فرض serverRoot آدرس /etc/apache2/ است که در خود فایل کانفیگ قابل تغییر است.
مثال آدرس include ports.conf این است:
```bash
root@mvm:~# ls /etc/apache2/ports.conf
```

محتویات فایل ports.conf:
```bash
Listen 80

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>
```
در این فایل می بینیم که پورت 80 در حال listen شدن است
و در صورت فعال بودن ماژول های SSL پورت 443 هم listen خواهد شد.

### Virtual Host
از ویرچوال هاست زمانی استفاده میکنیم که بخواهیم روی یک سرور چندین سایت بالا بیاریم.
![[Recording 20231103210133.webm]]


![[Pasted image 20231103205806.png]] 
![[Pasted image 20231103205852.png]]

یک ویرچوال هاست را برای نمونه ایجاد میکنیم:
1. برای این کار طبق توضیحات فایلی را در آدرس /etc/apache2/sites-available ایجاد میکنیم و بعد تک تک تنظیمات زیر را انجام میدهیم.
2. آدرس هایی که برای DocumentRoot , Errorlog , CoustomLog قرار میدهیم باید از قبل باید ساخته شده باشد.
3. در مسیر DocumentRoot یک فایل index.html ایجاد میکنیم.
4. سیمبلیک لینک مربوطه را در آدرس /etc/apache2/sites-enabled ایجاد میکنیم. برای این کار میتوانیم از دستور a2ensite استفاده کنیم و خود به خود سیبلینک لینک ایجاد میشود.
5. سرور را ریستارت یا ریلود میکنیم.
6. سرور DNS رو هم باید برای آدرس سایت جدید تنظیم کنیم.
![[Pasted image 20231103211209.png]]

> [!danger] هر رکوئستی که به سرور ارسال شود با هاستی که در سرور تعریف نشده و یا در صورتی که به جای هاست ip سرور در رکوئست باشد، اولین ویرچوال هاست نمایش داده می شود، بنابراین بهترین کار این است که اولین ویرچوال هاست را به هیچ وب سایتی اختصاص ندهیم.
