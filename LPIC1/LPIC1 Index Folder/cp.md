---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.3 Perform basic file management]]"
date: 2023-11-21
---
### copy
با این دستور از مبدا های مختلفی میتوانیم به یک مقصد کپی کنیم
با آپشن تی میتوانیم ابتدا مقصد را مشخص کنیم
با آپشن آر میتوانیم فولدرهای تو در تو را کپی کنیم
```bash
cp sourceS destination
cp -t destination sources 
cp -r sourceS destination
cp -t destination -r sources 
```
-v, --verbose
	explain what is being done
-r, --recursive
	copy directories recursively
-p
	same as --preserve=mode,ownership,timestamps
	مالیکت، پرمیشن ها و تایم استمپها همراه با فایل کپی می شوند
	در صورت عدم استفاده ازین آپشن فایل جدید ساخته می شود و مالک جدید برای فایل تعریف می شود
-i
	interactive : warning before overwrite


cp sourceS destination
cp -t destination sources 
