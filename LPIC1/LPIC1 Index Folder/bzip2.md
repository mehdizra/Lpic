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
bzip2  compresses  files  using  the Burrows-Wheeler block sorting text compression algorithm
   bzip2, bunzip2 - a block-sorting file compressor,v1.0.8
   [[bzcat]] - decompresses files to stdout
   bzip2recover - recovers data from damaged bzip2 files
-d:
با این آپشن فایل دیکامپرس می شود.
-c:
با این آپشن فایل دیتای کامپرس شده به خروجی استاندارد داده می شود که قابل ذخیره در فایل جدید است.
```bash
medme@vm1835730:~$ bzip2 mamad.txt
medme@vm1835730:~$ ls
mamad.txt.bz2
medme@vm1835730:~$ bzip2 -c mamad.txt > mamad.txt.bz2
medme@vm1835730:~$ bzip2 -cd mamad.txt.bz2 > new.txt
```
