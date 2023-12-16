---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[207.3 Securing a DNS server]]"
date: 2023-10-19
---
با این دستور کلیدی به اسم فو جنریت میکنیم
برای تست دو نمونه الگورتیم مختلف استفاده کردیم
```bash
root@mvm:~# tsig-keygen -a hmac-md5 foo
key "foo" {
        algorithm hmac-md5;
        secret "iyZvv5vg1yTv7cDjYBGMXw==";
};
root@mvm:~# tsig-keygen -a sha256 foo
key "foo" {
        algorithm hmac-sha256;
        secret "PN9fhYSilZ8A4N0QCUa2WUuA5lPVKDDQ5d0j0J2X9MQ=";
};
root@mvm:~#
```