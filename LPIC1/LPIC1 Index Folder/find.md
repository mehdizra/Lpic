---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.3 Perform basic file management]]"
date: 2023-11-21
---
### find [location]
```bash
find . # search for everything in working directory
find . | wc -l # number of everything in working directory
find . -type f # search in regular files in .
find . -type d # search in directories in .
find . -type l # search in symbolic links in .
find . -type b # search in block devices in .
find . -type c # search in character devices in .
find . -name "filename" # search for exact file name
find . -name "*lena*" # search for partial file name
find . -name \*lena\* # search for partial file name
find . -iname  # search incase sensitive
find . -notname  # search not this name
find / -type f -size 12M # search for every 12M file
find / -type f -size 12M 2> temp #search and save error output in a temp file
find / -type f -size 12M 2> /dev/null #search without error output
![[Recording 20231121200430.webm]]

![[Recording 20231121200507.webm]]
find / -type f -size +12M -size -15M # search for range size

```
ستاره را باید در کوتیشن یا همراه با اسلش استفاده کنیم چون کارکتر خاص بش است و بدون کوتیشن به دستور فایند اعمال نمی شود

### exec
اعمال دستورات بعدی روی موارد پیدا شده
![[Recording 20231121200028.webm]]
```bash
find / -type f -size +12M -size -15M -exec echo 1 \; 2>/dev/null
``` 

![[Recording 20231121200639.webm]]
```bash
find / -type f -size +12M -size -15M -exec ls -lh {} \; 2>/dev/null

find / -type f -name "*.txt*" -exec rm -vf {} \;
```
-v verbose
-f force 
{} place holder

![[LPIC 1 (session 4)#file stamps]]

-atime: access time stamp (per day)
-mtime: modify time stamp (per day)
-ctime: change time stamp (per day)
-amin: access time stamp (per min)
-mmin: modify time stamp (per min)
-cmin: change time stamp (per min)
```bash
find / -type f -mtime -1
فایلهایی که در یک روز گذشته تغییر کردند
find / -type f -mtime +1
فایلهایی که در یک روز گذشته تغییر  نکردند یعنی تغییرات مربوط به از 24 ساعت گذشته به قبل بوده اند
find / -type f -mtime 2 
فایلهایی که دقیقا 48 ساعت پیش تغییر کردند
find / -type f -amin -20
فایل هایی که 20 دقیقه پیش به آنها دسترسی داشتیم
```

### -delete
```bash
find . -name "*.bak" -delete # same as exec rm
با این آپشن میتوان فایلهایی که پیدا می شود را پاک کرد
```
