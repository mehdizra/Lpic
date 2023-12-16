---
tags:
  - LPIC
  - linux
  - command
up: "[[110.1 Perform security administration tasks]]"
---
###
```bash
sudo -i   # go to root shell
su mina # go to mina user Without password
```

```bash
mehdi@mvm:~$ cat /etc/shadow
cat: /etc/shadow: Permission denied
mehdi@mvm:~$ sudo cat /etc/shadow
[sudo] password for mehdi:
root:!:19568:0:99999:7:::
```
#### sudoers user example
```bash
mamad@mvm:~$ sudo ls
[sudo] password for mamad:
mamad is not in the sudoers file.  This incident will be reported.
```