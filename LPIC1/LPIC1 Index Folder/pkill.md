---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.5 Create, monitor and kill processes]]"
date: 2023-11-25
---
### pkill
NAME
       pgrep, pkill, pidwait - look up, signal, or wait for processes based on
       name and other attributes

SYNOPSIS
pgrep [options] pattern
	pgrep looks through the  currently  running  processes  and  lists  theprocess IDs which match the selection criteria to stdout.  All the criteria have to match.  For example :
		$ pgrep -u root sshd
	will only list the processes called sshd AND owned  by  root.   On  the other hand
		$ pgrep -u root,daemon
	will list the processes owned by root OR daemon.

pkill [options] pattern

   pkill  will  send  the  specified  signal  (by default SIGTERM) to each  process instead of listing them on stdout.

pidwait [options] pattern
   pidwait will wait for each process instead of listing them on stdout.

```bash
 pgrep -u root,daemon # لیست پردازش های یوزر مورد نظر
 pkill -u peyman # توقف پردازش های یوزر مورد نظر
```