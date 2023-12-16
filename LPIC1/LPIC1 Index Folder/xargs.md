---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.4 Use streams, pipes and redirects]]"
date: 2023-11-22
---
### xargs 
- build and execute command lines from standard input
```bash
medme@vm1835730:~$ cat folder_name
f001
f002
foo3
medme@vm1835730:~$ cat folder_name | xargs mkdir
medme@vm1835730:~$ ls
f001  f002  folder_name  foo3
```
این دستور یعنی فایل فولدر_نیم را بخون و پایپ کن به ایکس آرگس و از ابزار ایکس آرگز میخواهیم دستور ساخت دایرکتوری را با آرگومان های پایپ شده اجرا کند

برای پاک کردن
```bash
medme@vm1835730:~$ cat folder_name | xargs rm -r *
```