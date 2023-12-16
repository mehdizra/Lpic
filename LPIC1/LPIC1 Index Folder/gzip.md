---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.3 Perform basic file management]]"
date: 2023-11-18
---
###
با این دستور فایلها را زیپ میکنیم این برنامه از الگوریتم دیفلیت استفاده میکند.
-d:
با این آپشن فایل دیکامپرس می شود.
-c:
با این آپشن فایل دیتای کامپرس شده به خروجی استاندارد داده می شود که قابل ذخیره در فایل جدید است.

```bash
medme@vm1835730:~$ ls
mamad.txt
medme@vm1835730:~$ gzip mamad.txt
medme@vm1835730:~$ ls
mamad.txt.gz

medme@vm1835730:~$ gzip -d mamad.txt.gz
medme@vm1835730:~$ ls
mamad.txt

medme@vm1835730:~$ gzip -c mamad.txt > mamad.txt.gz

```