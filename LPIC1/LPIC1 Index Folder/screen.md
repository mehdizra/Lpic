---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.5 Create, monitor and kill processes]]"
date: 2023-11-25
---
### screen
screen sample
```bash
medme@vm1835730:~$ screen -ls # screen list
No Sockets found in /run/screen/S-medme.
medme@vm1835730:~$ screen -S myping # make a screen
medme@vm1835730:~$ ping 9.9.9.9
Ctrl+a+d # detach from screen
[detached from 4756.myping]
medme@vm1835730:~$ screen -ls
There is a screen on:
        4756.myping     (11/25/23 20:16:14)     (Detached)
1 Socket in /run/screen/S-medme.

medme@vm1835730:~$ screen -r 4756 # attach to screen
یا
medme@vm1835730:~$ screen -r myping # attach to screen
یا
medme@vm1835730:~$ screen -r # attach to screen if there is only 1 screen
ctrl+d # close the screen
[screen is terminating]
```
