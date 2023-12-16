---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[104.3 Control mounting and unmounting of filesystems]]"
date: 2023-11-16
---
### fstab
در این فایل مانت پوینت هایی که میخواهیم با ریبوت شدن مانت شوند را تعریف میکنیم. در صورت وجود اشتباه در این تنظیمات سیستم بوت نخواهد شد و باید این کار را با دقت انجام داد
هر خط در این فایل یک مانت است که شامل 6 ستون می شود که با space از هم جدا می شوند

```bash
root@vm1835730:~# vi /etc/fstab
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/vda2 during curtin installation
/dev/disk/by-uuid/245a527a-8970-4a87-bc16-ddfbde21408d / ext4 defaults 0 1
~ /dev/sdb1   /mnt/p1  vfat defaults 0 0
~ UUID="CSFF-0255" /mnt/p1  vfat defaults 0 0

```
1. نام دیوایس یا پارتیشن
2. آدرس مانت پوینت
3. نوع فایل سیستم
4. مانت آپشن ها که فعلا دیفالت میگذاریم
5. dump
6. pass
دامپ و پس را صفر قرار میدهیم

برای تست میتوانیم موارد داخل فایل را با دستور مانت و با یک آرگومان دیوایس یا مانت پوینت، مانت کنیم.

defaults,users
اگر یوزرز را به آپشن ها اضافه کنیم یوزرهای معمولی میتوانند مانت و آنمانت کنند

defaults,user
اگر یوزر را به آپشن ها اضافه کنیم هر یوزری که مانت کرده است فقط خودش میتواند آنمانت کند


> [!question] اگر جای پورت هارد دیسک ما تغییر کند، اینتری های این فایل درست مانت نخواهند شد. راهکار چیست؟
> استفاده از uuid
