---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.2 Process text streams using filters]]"
date: 2023-11-18
---
### zcat
همان دستور کت است که محتوای فایل های زیپ شده را به صورت موقت نشان میدهد و تغییری در فایل ایجاد نمیکند
### zgrep
همان دستور گرپ است که به دنبال آرگومان خود در فایل زیپ شده میگردد.
```bash
medme@vm1835730:~$ zcat mamad.txt.gz
ksjd
;alkjsd
d;aksjd

medme@vm1835730:~$ zgrep a mamad.txt.gz
;alkjsd
d;aksjd
```