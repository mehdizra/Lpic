---
tags:
  - LPIC
  - linux
  - concept
  - command
  - commandline
up: "[[LPIC1 Sessions map of content]]"
date: 2023-07-18
---
در این جلسه تمام دستورات فصل 3 کتاب اول را بررسی میکنیم:
### [[103.1 Work on the command line]]
[[bash]]
[[echo]]
[[env]]
[[export]]
[[pwd]] print working directory
[[set]]
[[unset]]
[[type]] show command type (internal/external)
[[which]] locate a command
[[man]] get command information
[[uname]] print system information
[[history]]
.[[bash_history]]
[[Quoting]] to escape special characters 

[[touch]] change file timestamp
[[apropos]]  search the manual page names and descriptions 

### [[103.2 Process text streams using filters]]
[[diff]] compare two text file
[[bzcat]] Uncompress FILEs to standard out
[[cat]]  concatenate files and print on the standard output
[[cut]] Print selected parts of lines from each FILE
[[head]] output the first part of files
[[less]] cat with scroll
[[more]] cat with down scroll
[[md5sum]] a checksum algorithm
[[nl]] number lines of files
[[od]] dump files in octal and other formats
[[paste]]
[[sed]]  stream editor for filtering and transforming text
[[sha256sum]] a checksum algorithm
[[sha512sum]] a checksum algorithm
[[sort]]
[[split]] split a file into pieces
[[tail]] output the last part of files
[[tr]]
[[uniq]]
[[wc]] word count
[[xzcat]] Uncompress FILEs to standard out
[[zcat]] , zgrep Uncompress FILEs to standard output.
### compression 
دو نوع الگوریتم فشرده سازی داریم.
- الگوریتم های lossy که فایل ها در آن پس از فشرده شدن قابل برگشت به حالت اول نیستند مثل mp3 ,jpeg ,divx
- الگوریتم های lossless که فایل ها در آن پس از فشرده شدن قابل بازگشت هستند مثل zip, png
#### الگوریتم deflate 
یک الگوریتم lossless است که برنامه های مختلفی ازین برنامه استفاده میکنند.
برنامه [[gzip]] از Zlib library استفاده میکند که این کتابخانه از الگوریتم deflate بهرمند است.
#### الگوریتم burrows wheeler
این الگوریتم شبیه الگوریتم دیفلیت است با سرعتی کمتر و میزان فشرده سازی بیشتر
در شرایطی که زمان در اولویت نباشد و میزان فشرده سازی مهم باشد ازین الگوریتم استفاده میکنیم. برنامه [[bzip2]] از این الگوریتم بهره می برد.

الگوریتم LZMA
این الگوریتم قویترین الگوریتم فشرده سازی است از لحاظ میزان فشرده سازی 
برنامه [[xz]] ازین الگوریتم بهره می برد.

> [!idea] فایل /var/log/btmp 
> فایلی است که لاگ تلاش های ناموفق برای ارتباط ssh به ماشین را در خود ذخیره میکند. 

> [!idea] زمان کامپرس و دیکامپرس
> الگوریتم های فشرده سازی هرچقدر قوی تر باشند زمان بیشتری برای کامپرس کردن صرف میکنند اما دیکامپرس بسیار سریعتر اتفاق می افتد. 

### check sum, digest , hash
الگوریتم های هش یا دایجست برای تبدیل کردن یک دیتا به یک خروجی با طول ثابت هستند. بنابراین نام آنها همراه با عددی است که بیانگر حجم بایت خروجی است.
به این عملیات encryption یا digest یا hash میگویند
کاربرد آنها برای مقایسه کردن دو فایل، استفاده در کلیدهای رمزنگاری، ذخیره رمزها در دیتابیس و موارد بسیار دیگری است.
دستورات [[sha512sum]] , [[sha256sum]] , [[md5sum]] با الگوریتم های مختلفی عملیات هش را انجام میدهند. و با آپشن -c میتوان دو summary را مقایسه کرد.
> [!idea] الگوریتم های هش کاملا یکطرفه است و قابل برگشت نیست.
> دیتابیس هایی هستند که مدام در حال ذخیره کردن عبارتهای مختلف به صورت هش هستند که برای شکستن رمزها از آن میتوان استفاده کرد. به این دیتابیس ها rainbow table گفته می شود.

> [!question] آیا داده های متفاوتی وجود دارند که خروجی هش در آنها یکسان باشد؟
> بله وجود دارند. به این اتفاق collision میگوییم.
> احتمال کولیژن در الگوریتمهایی که طول هش آنها بیشتر است کمتر می شود. 
> 

```bash
medme@vm1835730:~$ echo hello > new1
medme@vm1835730:~$ echo hello > new2
medme@vm1835730:~$ echo hello > new3
medme@vm1835730:~$ md5sum new*
b1946ac92492d2347c6235b4d2611184  new1
b1946ac92492d2347c6235b4d2611184  new2
b1946ac92492d2347c6235b4d2611184  new3
medme@vm1835730:~$ sha256sum new*
5891b5b522d5df086d0ff0b110fbd9d21bb4fc7163af34d08286a2e846f6be03  new1
5891b5b522d5df086d0ff0b110fbd9d21bb4fc7163af34d08286a2e846f6be03  new2
5891b5b522d5df086d0ff0b110fbd9d21bb4fc7163af34d08286a2e846f6be03  new3
medme@vm1835730:~$ sha512sum new*
e7c22b994c59d9cf2b48e549b1e24666636045930d3da7c1acb299d1c3b7f931f94aae41edda2c2b207a36e10f8bcb8d45223e54878f5b316e7ce3b6bc019629  new1
e7c22b994c59d9cf2b48e549b1e24666636045930d3da7c1acb299d1c3b7f931f94aae41edda2c2b207a36e10f8bcb8d45223e54878f5b316e7ce3b6bc019629  new2
e7c22b994c59d9cf2b48e549b1e24666636045930d3da7c1acb299d1c3b7f931f94aae41edda2c2b207a36e10f8bcb8d45223e54878f5b316e7ce3b6bc019629  new3
```

### [[103.3 Perform basic file management]]
[[cp]] copy files and directories with -r
[[find]] find sth in swh
[[mkdir]] make directory
[tree] show directory in tree form
[[mv]] move and rename
[[ls]] list directory content
[[rm]] delete files and directories with -r
[[rmdir]] delete directory if directory is empty 
[[touch]]  change file timestamps
[[tar]] make Archive file
[[cpio]] make Archive file
[[dd]]
[[file]]
[[gzip]] compression with deflate algorithm
[[gunzip]]
[[bzip2]] compression with burrows wheeler algorithn
[[bunzip2]]
[[xz]] most powerful compression algorithm 
[[unxz]]
[[file globbing]] expands a wildcard pattern into the list of pathnames matching the pattern

> [!idea] لینوکس یک سیستم عامل case sensitive است یعنی فایل یا فولدر همنام با وجود تفاوت در کوچکی و بزرگی حروف در آنها قابل ایجاد هستند
> 

> [!code] [[stat]] #command
> اطلاعات metadata فایل را نمایش میدهد 

در اینجا دو نمونه از فایل استت ها را میبینیم
```bash
medme@vm1835730:~$ stat /var/log/btmp
  File: /var/log/btmp
  Size: 35247360        Blocks: 68880      IO Block: 4096   regular file
Device: fc02h/64514d    Inode: 131300      Links: 1
Access: (0660/-rw-rw----)  Uid: (    0/    root)   Gid: (   43/    utmp)
Access: 2023-11-19 09:45:02.295780015 +0100
Modify: 2023-11-21 18:10:30.872608281 +0100
Change: 2023-11-21 18:10:30.872608281 +0100
 Birth: 2023-11-13 12:13:22.148000000 +0100

medme@vm1835730:~$ stat test.txt
  File: test.txt
  Size: 0               Blocks: 0          IO Block: 4096   regular empty file
Device: fc02h/64514d    Inode: 261684      Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/   medme)   Gid: ( 1000/   medme)
Access: 2023-11-21 18:07:52.230259413 +0100
Modify: 2023-11-21 18:07:52.230259413 +0100
Change: 2023-11-21 18:07:52.230259413 +0100
 Birth: 2023-11-21 18:07:52.230259413 +0100
```
file: file name
blocks: how many blocks use on disk
IO Block: block size
file type
Inode: Inode number on disk
Links: symbolic links
access: permission 
Uid: user ID
#### file stamps
Access: The last ==access== time of file (reading a file - not writing)
Modify: The last ==content edit== time of file
Change: The last ==attribute edit== or ==content edit== time of file
Birth: No support in most OS but if support, this is birth time of file and it never changed

> [!idea] دستور [[touch]] تمامی تایم استمپ ها را بروزرسانی میکند.
![[touch#options]]

#### Archiving Files
مفاهیوم آرشیو کردن و فشرده سازی دو مفهوم مجزا از هم هستند، با این حال نرم افزارهایی وجود دارند که همراه با آرشیو کردن فشرده سازی هم انجام میدهند.
آرشیو create  و extract می شود.
اما فایل فشرده compress و decompress می شود.
در لینوکس یکی از ابزارهای معروفی که کار آرشیو کردن به معنای تبدیل تعدادی فایل به یک فایل را انجام می دهد، دستور [[tar]] است.

### [[103.4 Use streams, pipes and redirects]]

[[xargs]] - build and execute command lines from standard input
گاها در شرایطی قرار میگیریم که تعداد آرگومانهایی که میخواهیم به یک دستور اعمال کنیم زیاد هستند و نمیتوانیم از پایپ لاین | استفاده کنیم. در این شرایط برنامه xargs به کمک ما می آید.

> [!question] چطور میتوانیم تمام فایل های .conf رو در یک فایل کامپرس کنیم.؟
```bash
find /etc -type f -name "*.conf*" | xargs tar -czvf config.tar.gz
```

[[tee]]  read from standard input and write to standard output and files
```bash
date | tee out.txt
```
خروجی یک کامند را علاوه بر نمایش میتوان در یک فایل ذخیره کرد