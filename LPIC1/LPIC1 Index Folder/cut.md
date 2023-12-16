---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.2 Process text streams using filters]]"
date: 2023-11-19
---
### cut
Print selected parts of lines from each FILE to standard output.
With no FILE, or when FILE is -, read standard input.

```bash
medme@vm1835730:~$ cat new1
ali: 23: zanjan
reza: 24: qom
maria: 21: tehran
medme@vm1835730:~$ cut -d: -f2 new1
 23
 24
 21
medme@vm1835730:~$ cut -d: -f3 new1
 zanjan
 qom
 tehran
medme@vm1835730:~$ cut -d: -f1 new1> new2
medme@vm1835730:~$ cat new2
ali
reza
maria

```