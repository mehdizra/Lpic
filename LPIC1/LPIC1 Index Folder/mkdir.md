---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.3 Perform basic file management]]"
date: 2023-11-20
---
###
دایرکتوری برای آخرین پارت آدرس ساخته میشود و با یک دستور نمیتوان دایرکتوری های تو در تو ایجاد کرد
make directory name: c with -p (parent)
```bash
medme@vm1835730:~$ mkdir a/b/c
mkdir: cannot create directory ‘a/b/c’: No such file or directory
medme@vm1835730:~$ mkdir -p a/b/c
medme@vm1835730:~$ tree
.
└── a
    └── b
        └── c

3 directories, 0 files
```
-v, --verbose
	explain what is being done
 -r, --recursive
	copy directories recursively