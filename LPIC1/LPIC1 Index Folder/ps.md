---
tags:
  - linux
  - command
up: "[[103.5 Create, monitor and kill processes]]"
---
```bash
ps
```
این دستور به تنهایی لیست پردازش هایی که پرنت آن شل جاری است را نشان میدهد

این دستور جزو دستورات قدیمی است و سه دسته آپشن با قابلیت های تکراری دارد
 This version of ps accepts several kinds of options:

1   UNIX options, which may be grouped and must be preceded by a dash.
2   BSD options, which may be grouped and must not be used with a dash.
3   GNU long options, which are preceded by two dashes.

برای دیدن تمامی پراسس ها هر دو آپشن زیر کار میکند
```bash
ps aux # این آپشن بدون خط تیره است
ps -e # لیست تمام پردازش ها
ps -ef # لیست تمام پردازش ها با اطلاعات تکمیلی در فرمت استاندارد
ps -eo # لیست تمام پردازش ها در فرمت اختیاری
```
