---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[205.2 Advanced Network Configuration]]"
date: 2023-10-15
---
در سناریوی زیر میخواهیم ترافیک بین کارت شبکه ماشین خودمان و سرور 4.2.2.4 را بررسی کنیم
ابتدا اسم اینترفیس شبکه را میخواهیم

```bash
mehdi@mvm:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:61:41:4b brd ff:ff:ff:ff:ff:ff
    altname enp2s1
    inet 192.168.243.128/24 brd 192.168.243.255 scope global dynamic noprefixroute ens33
       valid_lft 1600sec preferred_lft 1600sec
    inet6 fe80::df24:517c:9fdc:6f8/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
mehdi@mvm:~$ sudo tcpdump -ni ens33 host 4.2.2.4
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on ens33, link-type EN10MB (Ethernet), snapshot length 262144 bytes
12:16:43.414838 IP 192.168.243.128.40723 > 4.2.2.4.53: 23682+ [1au] A? ubuntu.com. (51)
12:16:43.529335 IP 4.2.2.4.53 > 192.168.243.128.40723: 23682 3/0/1 A 185.125.190.21, A 185.125.190.29, A 185.125.190.20 (87)
```