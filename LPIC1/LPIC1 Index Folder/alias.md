---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[105.1 Customize and use the shell environment]]"
date: 2023-11-24
---
### alias
مثل شورتکات در ویندوز عمل میکند
این دستور به تنهایی لیست الیاس ها را نشان میدهد.

```bash
alias
```

مثال : برای دستور پینگ یک الیاس تعریف کنیم
```bash
alias p="ping -c4 9.9.9.9"
```

برای استفاده از الیاسها پس از خروج و ورود مجدد به بش باید آنها را در فایل بش آر سی در پوشه هوم ذخیره کنیم.
[[bashrc]]
```bash
vim ~/.bashrc
alias p="ping -c4 9.9.9.9"
```
یا
```bash
medme@vm1835730:~$ alias p=\"ping -c4 9.9.9.9\" >> .bashrc
```
برای در دسترس قرار دادن یک الیاس برای همه یوزر ها آن را در آدرس زیر قرار می دهیم.
[[etc bash.bashrc]]
```bash
vim /etc/bash.bashrc
```