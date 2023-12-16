---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.3 Perform basic file management]]"
date: 2023-11-22
---
### list

```bash
ls
```

-l     use a long listing format
-r, --reverse
	  reverse order while sorting
-R, --recursive
	  list subdirectories recursively
-h, --human-readable
	  with -l and -s, print sizes like 1K 234M 2G etc.
-a, --all
	  do not ignore entries starting with .
-A, --almost-all
	  do not list implied . and ..
### انواع فایل
وقتی از آپشن ال استفاده میکنیم حرف اول هر آیتم بیانگر نوع اون آیتم است
```bash
ls -l /etc 
lrwxrwxrwx 1 root root      13 Feb 15  2023 rmt -> /usr/sbin/rmt
drwxr-xr-x 2 root root          60 Nov 25 12:03 virtio-ports
```
l = symbolic link
d = directory 
b = block device (block special device)
