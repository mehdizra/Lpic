---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[LPIC1 Sessions map of content]]"
date: 2023-10-03 - 1401-07-11
---
### تسکت ادیتور [[vi]]
این تکست ادیتور یکی از قدیمی ترین و معروف ترین تکست ادیتورهای لینوکس است که کاربردهای مختلفی در لینوکس دارد.
کارکردن با این تکست ادیتور راحت نیست و میانبرهای زیادی دارد.

> [!code] [time]  #command
> اگر بخواهیم ببینیم اجرای یک دستور در لینوکس چقدر طول میکشد از دستور تایم استفاده میکنیم و دستور مورد نظر رو به عنوان آرگومان به این دستور پاس می دهیم مثلا

```bash
time ls
real    0m0.026s
user    0m0.025s
sys     0m0.001s
```

> [!idea] در لینوکس به پراسس هایی که به اتمام نمی رسند و مدام در حال اجرا هستند service یا deamon گفته میشود.  مثل webserver یا database
> 
### متغیر ?
هر دستوری در bash پس از اجرا یک عددی را به bash ارسال میکند که تعیین میکند که آیا آن دستور به درستی اجرا شده یا با خطا مواجه شده است. این عدد در متغیر ? ذخیره می شود و در صورتی که بعد از اجرای دستور این مقدار این متغیر صفر باشد یعنی دستور به درستی اجرا شده است.
از مقدار این متغیر در اسکریپت نویسی استفاده می شود.
```shell
ls
echo $?
```
> [!idea] اگر فایل مورد نظر وجود نداشته باشد یا مجاز نباشد عدد 2 در متغیر ذخیره میشود.

### اجرای چند کامند 
برای اجرای چند کامند روشهای مختلفی وجود دارد.
**جدا کننده |** 
دو دستور با این جدا کننده جدا شوند همزمان اجرا می شوند
اما خروجی کامند اول به ورودی کامند دوم ارسال می شود.
**جدا کننده ;**
دو دستور با این جدا کننده به ترتیب اجرا می شوند. اجرای این دو دستور ارتباطی بهم ندارد.
**جدا کننده &&**
دو دستور با این جدا کننده به ترتیب اجرا می شوند، به شرطی که کامند اول به درستی اجرا شده باشد و status code آن صفر بوده باشد.
**جدا کننده ||**
فقط دستور اول اجرا می شود و اگر با خطا مواجه شود (status code غیر از صفر داشته باشد)، دستور دوم اجرا خواهد شد. 

#### ریدایرکت
همانطور که گفته شد برای ریدایرکت کردن از علامت بزرگتر < استفاده میکنیم که در صورت استفاده از آن اطلاعات روی فایل overwrite می شود اما اگر از << استفاده کنیم به فایل اضافه یا append می شود.
اما ما دو خروجی داریم: خروجی استاندارد و خروجی ارور
برای ریدایرکت خروجی استاندارد باید از <1 استفاده کنیم و برای ریدایرکت خروی ارور از <2 استفاده می کنیم.
بش به صورت پیش فرض فقط خروجی استاندارد را ریدایرکت میکند یعنی < با <1 فرقی ندارد.


> [!question] در صورتی که بخواهیم خروجی استاندارد و ارور را همزمان ریدایرکت کنیم از چه دستوری باید استفاده کنیم؟ 
با این دستور به بش میگوییم که لیست خانه و روت را بگیر آن را به فایل out ریدایرکت کن و در صورت ارور آن را به همانجا که خروجی استاندارد را ریدایرکت کردی ریدایرکت کن.
```bash
student@s14:~$ ls $HOME root > out 2>&1
```

#### آپشن ها
دستورات در لینوکس اغلب همراه با آپشن همراه می شوند
این آپشن ها کوتاه یا تک حرفی و بلند هستند
برای استفاده از آپشن های کوتاه از - و برای استفاده از آپشن های بلند از -- استفاده میکنیم.

#### دستور grep
> [!code] [[grep]] برای فیلتر کردن یک عبارت در ورودی و یا در یک فایل یا از خروجی استاندارد از این دستور استفاده می کنیم.  
> #command 

```bash
student@s14:~$ grep salam # گرپ از ورودی
salam
salam

student@s14:~$ cat out
ls: cannot access 'root': No such file or directory
/home/student:
out
out2
salam.py
student@s14:~$ grep salam out # گرب از فایل
salam.py

student@s14:~$ ls / 
bin   dev  home  lib32  libx32      media  opt   root  sbin  srv       sys  usr
boot  etc  lib   lib64  lost+found  mnt    proc  run   snap  swap.img  tmp  var
student@s14:~$ ls / | grep bin  # گرب از خروجی
bin
sbin
```


> [!question] این سه دستور نتیجه یکسان دارند. کدام دستور متفاوت از بقیه است؟
> grep linux < test.txt
> grep linux test.txt
> cat test.txt | grep linux
> جواب: گزینه دوم چرا که در دو دستور دیگر فایل باز می شود و به عنوان خروجی به ورودی گرپ داده می شود اما در گزینه دوم خود گرپ فایل را باز میکند.


> [!question] چرا در دستورات زیر فقط پاسخ اول همراه با نام فایل است؟
> جواب چون فقط در دستور اول یک فایل out را خواندیم و در دو دستور بعدی فایل out را به عنوان خروجی به ورودی word count دادیم.
```bash
student@s14:~$ wc -l out
5 out
student@s14:~$ wc -l < out
5
student@s14:~$ cat out | wc -l
5
```

##### آپشن های گرپ
-i به معنای ignore case یعنی بزرگی و کوچکی حساس نخواهد بود
-v به معنای invert match یعنی به دنبال غیر از کلمه مورد نظر میگردد
-c به معنای count یعنی به دنبال تعداد می گردد.
-n به معنای line number یعنی شماره خط رو هم پیدا میکند.

با گرپ می توانیم چندین فایل را همزمان جستجو کنیم.

> [!search] در صورت نیاز، grep samples جستجو شود. 

> [!idea] In Linux everything is a file 

> [!code] [[ping]] برای بررسی ارتباط با یک اینترفیس ازین دستور استفاده میکنیم.  
> #command

> [!idea] برای تمرین لینوکس در سطوح مختلف به خصوص امنیت میتوانیم از سایت بازی-آموزشی [overthewire](https://overthewire.org) استفاده کنیم.

### Globbing
گلابینگ چیزی شبیه رجکس است که در زمان مسیر دهی استفاده می شود. صفحه [[file globbing]] مطالعه شود.
**پروسه های گلابینگ توسط بش اتفاق می افتد.**

> [!search] در صورت نیاز، File Globbing یا bash Globbing جستجو شود. 
> 

دستورات sort و uniq یا باید تمرین کنیم. 

### پارتیشن بندی
برای دیدن هارد دیسک ها و پارتیشن های هر هارد میتوانیم از دستور زیر استفاده کنیم.
```bash
ls /dev/sd* -l
```
هاردهای اسکازی, USB یا  SATA باشند با sd شروع می شوند و هاردهای ide با hd شروع می شوند.

> [!idea] پارتیشن بندی در لینوکس از سه روش اتفاق می شود: MBR GPT LVM

#### روش MBR
قدیمی ترین روش پارتیشن بندی روش [[MBR]] به معنای Master boot record که اطلاعات پارتیشن را در سکتور صفر نگه میدارد.
- هر سکتور 512 بایت که 446 بایت از سکتور صفر در روش MBR بوت لودر قرار میگیرد، 2 بایت رزرو است و 64 بایت باقی مانده برای اطلاعات Partition table است. 
- اطلاعات در partition table شامل سه بخش است: سکتور شروع ، سکتور پایان، و تایپ پارتیشن
- در روش mbr ما نهایتا 4 پارتیشن میتوانیم داشته باشیم که علت آن فضای کم partition table است
- یکی از پارتیشن های mbr را میتوانیم با type ID 5 یا Extended معرفی کنیم و در داخل آن 10 پارتیشن مجازی تعریف کنیم.
- اطلاعات partition table پارتیشن های مجازی در سکتور اول همان پارتیشن extended ذخیره میشود.
- برای استفاده از MBR ما از ابزار [[fdisk]] استفاده می کنیم. اما ابزارهای پیشرفته تری هم هست که میتوان از آنها هم استفاده کرد.
> [!search] در صورت نیاز، روش [[parted]] یا mbr support partition tools سرچ شود. 

دستور [[fdisk]]
با دستور fdisk و آدرس یکی از پارتیشن ها به عنوان آرگومان میتوانیم وارد محیط fdisk شویم. و با کلید m نحوه کار آن را ببینیم
```bash
Command (m for help): p

Disk /dev/sda: 100 GiB, 107374182400 bytes, 209715200 sectors
Disk model: Virtual disk    
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 4EE2C4F2-270A-41B1-9307-1DA0A1AE4E89

Device       Start       End   Sectors Size Type
/dev/sda1     2048      4095      2048   1M BIOS boot
/dev/sda2     4096   4198399   4194304   2G Linux filesystem
/dev/sda3  4198400 209713151 205514752  98G Linux filesystem
```

ساختن پارتیشن خیلی با MBR خیلی ساده است.
n پارتیشن جدید ایجاد میکند
d پارتیشن حذف میکند.
q خروج از برنامه
w تمام تغییرات را رایت میکند.
نهایتا 4 پارتیشن primary میتوان ساخت
و پارتیشن های logical از شماره 5 به بعد شروع می شوند که آنها در دل پارتیشن extended قرار دارند.

> [!idea] پارتیشن بندی MBR زیاد مورد پسند نیست. به دلیل ضعف هایی که دارد.
> 1. دیسک بالای 2 ترابایت را نمی تواند پارتیشن بندی کند
> 2. تعداد پارتیشن های محدودی را میتوان در آن تعریف کرد.
#### روش GPT
مخفف GUID partition table است.
این روش یک partition table جدید است که در ویندوز و لینوکس کار میکند اما با ویندوز بوت نمی شود.
- تفاوتش با mbr در این است که فضای بیشتری برای partition table در نظر می گیرد.
- در GPT ما میتوانیم 128 پارتیشن داشته باشیم.
- تایپ id در این پارتیشن بندی 2 بایتی است.
- برای این پارتیشن بندی از دستور gdisk استفاده میکنیم.4

برنامه [[gdisk]]
بسیار شبیه دستور fdisk است.

پس از پارتیشن بندی و ذخیره تغییرات باید پارتیشن را فورمت کرد و آن را به یک آدرس مانت کرد که قابل استفاده باشد.

> [!code] [[mkfs]] برای فرمت کردن پارتیشن ازین دستور استفاده میکنیم.
> make file system  
> #command

> [!question] چطور میتوانیم پارتیشن های فورمت شده را ببینیم؟
> با دستور [[blkid]] پارتیشن های موجود را می بینیم و مواردی که فورمت شدند شامل UUID و TYPE فورمت هستند.

ما فایل سیستم های بیشماری داریم. هر فایل سیستم قابلیت های مختلفی دارد که با توجه به کاربرد و شرایط باید انتخاب شود. مثل:
vfat, xfs, ext4, ext2, ntfs
برای کاربردهای مختلف از فایل سیستم های مختلف استفاده میکنیم
- بالانس ترین فایل سیستم در حال حاضر ext4 است بنابراین اگر کاربری پارتیشن مشخص هم نباشد از همین مورد استفاده میکنیم.
- در مواردی که فایل های با حجم کم و تعداد بالا وجود دارد reiserfs مناسب تر است.
- یا در مواردی با فایلهای با حجم بسیار بالا xfs مناسب تر است.

### مانت کردن پارتیشن
هر فایل سیستمی به شکل خاصی فایل ها رو در پارتیشن رایت میکند. در هر پارتیشن یک سری 0 و 1 هست که برای ما قابل فهم نیست، ما با کمک فایل سیستم پارتیشن را به یک دایرکتوری مانت میکنیم که فایل های داخل پارتیشن برای ما قابل دسترس شود
- این اتفاق در همه سیستم عامل ها رخ می دهد. مثلا در ویندوز دایرکتوری هایی که پارتیشن به آنها (به صورت خودکار) مانت می شود drive letter نام دارد.
- به این دایرکتوری ها mount point یا نقطه اتصال گفته می شود.
- خود دایرکتوری / یک نقطه اتصال است که پارتیشنی که روی آن لینوکس نصب شده به آن مانت شده است و بقیه پارتیشن ها به دایرکتوری هایی زیرمجموعه / مانت خواهند شد
- معمولا برای مانت پویت از یک دایرکتوری خالی استفاده میکنیم.
- در صورت وجود محتوا در دایرکتوری مانت پوینت، پس از مانت، آن محتوا دیگر نمایش داده نمیشود تا زمانی که دوباره آنمانت شود.
- به صورت پیش فرض فولدری به نام mnt برای ایجاد مانت پوینت ها وجود دارد.
- برای مانت از دستور [[mount]] استفاده میکنیم.
- برای آنمانت از دستور [[umount]] استفاده میکنیم.

> [!question] لیست پارتیشن های مانت شده را چطور ببینیم؟
> 1. دستور mount با کمک گرپ sdb
> 2. دستور df 
> تفاوت این دو دستور در این است که با دستور mount مانت آپشن ها را هم میبینیم اما با دستور [[df]] سایز پارتیشن رو می بینیم


> [!question] چطور مانت ها را persist کنیم که با ریبوت آنمانت نشوند.؟
> با استفاده از فایل fstab

کانفیگوریشن و تنظیمات لینوکس اغلب در فایل ها هستند.
#### فایل [[fstab]]
در این فایل مانت پوینت هایی که میخواهیم با ریبوت شدن مانت شوند را تعریف میکنیم. در صورت وجود اشتباه در این تنظیمات سیستم بوت نخواهد شد و باید این کار را با دقت انجام داد
برای تست میتوانیم موارد داخل فایل را با دستور مانت و با یک آرگومان دیوایس یا مانت پوینت، مانت کنیم.

##### مانت آپشن ها
```bash
mount /dev/sdb1 /mnt/p1 -o ro
```
این آپشن باعث میشود مانت پوینت readonly باشد
درصورتی که بخواهیم بدون آنمانت کردن آپشن مانت را تغییر دهیم از آپشن remount استفاده می کنیم
```bash
mount /dev/sdb1 /mnt/p1 -o rw,remount
```
آپشن ها را در خود دستور mount میتوانیم ببینیم

> [!search] در صورت نیاز، linux general mount options سرچ شود. 

> [!idea] UUID که در فایل fstab هم استفاده می شود پس از فورمت شدن برای پارتیشن جنریت می شود و با هر بار فورمت شدن تغییر میکند.
بهتر است برای جلوگیری از اشتباه در مانت کردن از UUID به جای نام دیوایس پارتیشن استفاده کنیم.

در هر پارتیشن ext یک فلودر به نام lost+found به صورت خودکار ساخته می شود برای ریکاوری فایلهای از دست رفته.