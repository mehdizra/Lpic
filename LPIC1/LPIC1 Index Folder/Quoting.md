---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.1 Work on the command line]]"
date: 2023-11-18
---
### 
to escape special characters

```bash
mkdir a b c
mkdir 'a b c'
mkdir a\ b\ c
mkdir "a b c"
echo "$PATH"
```
فاصله در لینوکس کارکتر خاص است
برای نادیده شدن کارکترهای خاص از سه روش میتوان استفاده کرد
استفاده از کوتیشن
استفاده از اسلش
استفاده از دابل کوتیشن 
البته دابل کوتیشن برخی کارکترها را همچنان خاص درنظر میگرد مثل دلارساین