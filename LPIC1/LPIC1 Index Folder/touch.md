---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.3 Perform basic file management]]"
date: 2023-11-17
---
### touch
**کار اصلی** این دستور این است که تاریخ آخرین تغییر فایل به روز شود.
file time stamps

اما اگر فایلی وجود نداشته باشد با این دستور آن فایل ساخته می شود. اما با علامت بزرگتر هم میتوان فایل جدید ساخت

```bash
touch oldfile # change file timestamp or change last modification time
touch newfile.txt # make new file
> newfile2 # make new file
```

### options
touch -a : update only access time
touch -m: update only modified time