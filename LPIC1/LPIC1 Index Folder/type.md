---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.1 Work on the command line]]"
date: 2023-11-18
---
show command type : internal or built-in commands and external command

```bash
medme@vm1835730:~$ type ls
ls is aliased to ls --color=auto
medme@vm1835730:~$ type uname
uname is hashed (/usr/bin/uname)
medme@vm1835730:~$ type echo
echo is a shell builtin

medme@vm1835730:~$ type type
type is a shell builtin
medme@vm1835730:~$ man type
No manual entry for type
```
-t
```bash
type -t command # show comman type in one word
```