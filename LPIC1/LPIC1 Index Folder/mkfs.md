---
tags:
  - LPIC
  - command
  - concept
up: "[[104.1 Create partitions and filesystems]]"
date: 2023-11-16
---
-t برای انتخاب فایل سیستم از این آپشن استفاده میکنیم.

```bash
mkfs -t ext4 /dev/sdb1
mkfs -t ext2 /dev/sdb2
mkfs -t ntfs /dev/sdb3
mkfs -t reiserfs /dev/sdb4
mkfs -t xfs /dev/sdb4
```