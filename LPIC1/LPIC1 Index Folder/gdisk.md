---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[104.1 Create partitions and filesystems]]"
date: 2023-11-16
---
###

```bash
root@s14:~# gdisk /dev/sdc
GPT fdisk (gdisk) version 1.0.8

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.

Command (? for help): ?
b  back up GPT data to a file
c  change a partition s name
d  delete a partition
i  show detailed information on a partition
l  list known partition types
n  add a new partition
o  create a new empty GUID partition table (GPT)
p  print the partition table
q  quit without saving changes
r  recovery and transformation options (experts only)
s  sort partitions
t  change a partition s type code
v  verify disk
w  write table to disk and exit
x  extra functionality (experts only)
?  print this menu

```