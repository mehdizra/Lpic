---
tags:
  - LPIC
  - linux
  - command
  - process
up: "[[LPIC1 index map of content|LPIC1 index map of content]]"
date: 2023-11-24
---
### CPU timing 
یک CPU در آن واحد نمی تواند بیشتر ازیک process را اجرا کند.
بنابراین برای اجرای تعداد زیادی process هم زمان نیاز به راهکارهایی داریم.
علاوه بر استفاده از چندین CPU برای یک ماشین، صف بندی زمان CPU راهکار مهم دیگری است که این تصور را ایجاد می کند که پردازش ها در حال اجرای همزمان هستند.
### scheduling
زمانی که یک process میتواند از CPU استفاده کند را توسط Kernel به بخشهای کوچکی در حدود میلی ثانیه اما یک اندازه واحد تقسیم میکند.
به واسطه یک الگوریتم از بین process های در حال اجرا یک گزینه را انتخاب میکند و اصطلاحا time slot بعدی را به آن اختصاص می دهد.
این process به طور معمول در این timeframe انجام می شود اما اگر پردازش طولانی تر از timeframe بود دوباره در لیست پردازش های در حال اجرا قرار میگیرد تا دوباره نوبت به آن برسد.
کرنل با این مکانیزم اصطلاحا کرنل را به پردازش ها اجاره می دهد.

> [!search] در صورت کنجکاوی، CPU scheduling جستجو شود؟ 

> [!question] با توجه به اینکه خود kernel یک پردازش است چطور این عملیات را انجام می دهد؟
> کرنل هر بار که تصمیم میگیرد CPU را در اختیار یک پردازش قرار دهد خودکشی می کند و کل CPU را واگذار میکند اما با استفاده از یک register دوباره بیدار می شود و کنترل را در اختیار می گیرد.

### Process Attributes 
#### PID
یک عدد یکتاست که به هر پردازش اختصاص داده می شود.
#### Parent PID
عدد یکتایی است که متعلق به پردازش والد هر پردازش است
#### Status
یک پردازش وضعیت های مختلفی می تواند داشته باشد که با یک حرف مشخص می شود:
	R: (running) پردازشی است که در cpu در حال اجراست
	S: (sleep) زمانی پردازش در حالت خواب است یعنی نوبت متعلق به او نیست (به معنای توقف app نیست)
	T: (stop) زمانی که پردازش متوقف شده است این توقف میتواند با دستوراتی توسط یوزر انجام شود 
#### Owner
یوزری که پردازش را اجرا کرده است. دسترسی های یک پردازش از دسترسی های owner پردازش مشخص می شود.
#### Priority 
این که CPU به کدام پردازش ها time slot های بیشتر یا کمتری را بدهد به واسطه اولویت اون پردازش مشخص می شود.
عدد priority هر چقدر بالاتر باشد اولویت اون پردازش کمتر است.
#### Start time
زمانی که پردازش شروع شده است.
### init
- تنها پردازشی است که Parent ندارد اما این پردازش parent همه پردازش های دیگر است.
- عدد PID این پردازش همیشه 1 است.

## دستورات مربوط به پردازش ها

> [!code] [[ps]] با این دستور پردازش های در حال اجرا را می بینیم. #command
> در امتحان ازین مبحث سوال می آید.

![[Pasted image 20231124175252.png]]
دستور ps -ef ستون های مختلفی را نمایش می دهد.
- ستون UID : owner
- ستون PID : process ID
- ستون PPID : parent PID
- ستون STIME : start time
- ستون TTY : process from terminal(ssh)
- ستون TIME : process duration
- ستون CMD : process command

> [!question] چرا زمانی که از دستور ls استفاده میکنیم در لیست پردازش ها ls --color=auto رو می بینیم؟
> چون ls یک [[alias]] است برای  ls --color=auto 
### دستورات تو در تو
با استفاده از بک تیک \`  \` میتوانیم خروجی یک دستور را در ورودی یک دستور دیگر قرار دهیم.
> [!question] تفاوت بک تیک و پایپ لاین در چیست؟ 
### kill
> [!code] [[kill]]  #command 
> این دستور برای ارسال سیگنال به پردازش هاست.
> و معروفترین سیگنال شماره 15 به معنای TERMSIG و برای متوقف کردن پردازش است.
### graceful terminate  
این مدل از سیگنال ها که به graceful معروف هستند به پردازش مورد نظر سیگنالی ارسال میکنند که خودش در اسرع وقت متوقف شود. این امکان وجود دارد که پردازش آخرین تغییرات خود را قبل از توقف ذخیره کند.
> [!question] تفاوت سیگنال 15 و 2 دستور kill در چیست؟
> در عمل تفاوتی ندارند و هر دوی آنها به پردازش اجازه می دهند که پس از انجام آخرین محاسبات متوقف شوند اصطلاحا graceful terminate شوند اما برنامه نویسان میتوانند برای دریافت هر کدام از این سیگنال ها عملکرد متفاوتی را پیاده سازی کنند.
 مثلا دستور ping با هر دو سیگنال متوقف می شود اما با سیگنال 2 که همان ctrl+C است گزارش عملکرد خود را هم میدهد.

> [!question] تفاوت سیگنال 9 با 15 و 2 دستور kill در چیست؟
> سیگنال 9 یک ungraceful terminate است و دستور توقف را به خود پردازش واگذار نمیکند بلکه توقف پردازش مورد نظر از طرف کرنل انجام می شود.
> و فرصتی برای ذخیره تغییرات توسط پردازش نخواهد بود.

> [!code] [[killall]]  #command
> با این دستور میتوان یک پردازش را با آرگومان اسم اون پردازش متوقف کرد و به صورت پیشفرض سیگنال 15 به آن ارسال میشود.

> [!code] [[pkill]]  #command و [[pgrep]] و [[pidwait]]
> این دستور برای ارسال سیگنال پیشفرض به لیستی از پردازشهاست که آنها را با الگوی خاصی پیدا میکنیم.

> [!code] [[top]] , [[htop]]  #command 
> هر دو دستور برای مشاهده پردازش های ماشین به صورت زنده هستند.
> و قابلیت ارسال سیگنال و مشاهده گزارشهای مختلف در آنها وجوددارد.

> [!question] در سیگنالهای kill شماره 18 و 19 چیست؟
> 18 continue و 19 stop 
> 


### CPU Overloading
load average شامل 3 عدد می شود که میانگین استفاده از CPU در 1 و 5 و 15 دقیقه گذشته را نمایش می دهد.
در صورتی که 1 CPU داشته باشیم و در 1 دقیقه گذشته 100% آن در حال مصرف بوده باشد عدد اول 1 نمایش داده می شود.
در صورتی که همچنان 1 CPU داشته باشیم و  عدد اول 2 باشد یعنی در 1 دقیقه گذشته، دو برابر ظرفیت CPU پردازش داشتیم.
در صورتی که 2 CPU داشته باشیم و عدد اول 2 باشد یعنی در 1 دقیقه گذشته به اندازه 100% ظرفیت CPU پردازش داشتیم.

![[Pasted image 20231125160653.png]]

![[Recording 20231125160550.webm]]

> [!question] یک دستور بنویسید که تمام ظرفیت cpu را اشغال کند؟
> 
```bash
dd if=/dev/zero of=/dev/null
``` 

> [!code] [[uptime]]  برای مشاهده load average ازین دستور استفاده میکنیم. 
> #command

> [!code] [[watch]] #command 
> با این دستور میتوان یک دستور دیگر را با اینتروال پیش فرض 2 ثانیه مشاهده کرد.
```bash
watch uptime
```
## priority
اولویت در خروجی top یا htop با ستونی به نام PRI نمایش داده می شود که بیانگر اولویت هر پردازش است.
این عدد، عددی است بین 0 الی 39 که وسط آن 20 است.
وقتی یوزر های عادی پردازشی را اجرا میکنند با اولویت پیش فرض 20 شروع می شود. و این عدد با نزدیک شدن به 0 اولویت بیشتری خواهد داشت و با نزدیک شدن به 39 اولویت کمتری خواهد داشت.
برای تغییر اولویت پیش فرض از دستور [[nice]] قبل از command استفاده میکنیم که رنج اعداد آن از -20 الی 19 است. 
برای تغییر اولویت دستوراتی که در حال اجرا هستند از [[renice]] استفاده میکنیم.

> [!code] [[dd]]  #command
> این دستور برای انتقال بایت به بایت یک فایل یا یک پارتیشن به جای دیگر که اصطلاحا به آن image گرفتن گفته می شود.

### sudo files
دو sudo file داریم که کارایی های مختلفی دارند.
/dev/zero
یک بلاک دیوایس است که به صورت مجازی بی نهایت 0 روی آن ذخیره شده است.
/dev/null 
یک بلاک دیوایس است که هر چیزی که روی آن رایت شود از بین می رود.
```bash
dd if=/dev/zero of=/dev/null
```
این دستور از هیچ ایمیج میگیرد و به روی هیچ رایت میکند، و کاربرد آن اشغال کردن عمدی CPU است.

> [!code] [[free]] #command 
> این دستور با آپشن -m میزان مموری خالی را نمایش میدهد.
> این اطلاعات را از فایلی به آدرس زیر بازخوانی میکند. 
> /proc/meminfo

> [!question] swap چیست؟
![[Pasted image 20231125205247.png]]
![[Recording 20231125205223.webm]]

### job control
اگر کنسول cli لینوکس امکان اجرای فقط یک دستور را داشت، کارکردن برای یک ادمین خیلی سخت می بود، بنابراین راه کارهایی وجود دارد که میتوانیم برنامه ها را در background یا foreground جابجا کنیم که به این عملیات job control میگوییم. 
> [!code] [[&]] #command
> این دستور پردازش را به بک گراند ارسال میکند و اجازه میدهد روی پردازش های دیگر کار کنیم.

```bash
medme@vm1835730:~$ sleep 1000 &
[1] 3251
medme@vm1835730:~$ sleep 2000 &
[2] 3252
medme@vm1835730:~$ jobs
[1]-  Running          sleep 1000 &
[2]+  Running          sleep 2000 &
medme@vm1835730:~$ fg 1
sleep 1000
^C
medme@vm1835730:~$ fg
sleep 2000
```
به برنامه های در background میگوویم job
در مقابل هر job دو عدد jobID و PID وجود دارند که میتوانیم از آنها استفاده کنیم.

> [!code] [[jobs]] #command
> این دستور لیست برنامه های در حال اجرا در background را نمایش میدهد.

> [!code] [[fg]] #command
> این دستور بهمراه jobID مورد نظر آن پردازش را به foreground می آورد و میتوانیم با Ctrl+c سیگنال int به آن ارسال کنیم.
> این دستور بدون عدد jobID، آیتمی را که در مقابل آن + است را به foreground منتقل میکند.

> [!code] [[bg]] #command
> با این دستور میتوانیم یک پردازشی را که در background با ارسال سیگنال 19 یا کلیدهای Ctrl+z متوقف (stop) شده است را continue کنیم.

> [!question] چرا پردازشی که با سیگنال 19 یا Ctrl+z متوقف شده است با دستور bg ادامه می یابد؟
> چون bash نمیتواند پردازش stop شده را در foreground نگه دارد و آن را به background انتقال میدهد.
> 

> [!code] [[pstree]]  #command 
> این دستور process ها را به صورت درختی نمایش میدهد.

### virtual terminal
با دستور pstree می بینیم که وقتی به یک ماشین SSH میزنیم پردازش bash زیرمجموعه SSH است و در صورت kill شدن SSH قاعدتا child process ها هم از بین می روند. 
![[Pasted image 20231125223219.png]]

برای جلوگیری از kill شدن child process ها از مفهومی به نام virtual terminal استفاده می کنیم 
#### Screen
با دستور [[screen]] یک صفحه جدید باز می شود و این امکان را می دهد که در یک پردازش bash جدید فعالیت کنیم و قبل از بستن SSH آن را Detach و پس از بازگشتن مجددا آن را Attach کنیم که از فعالیت هایمان از بین نرود.
![[Pasted image 20231125223127.png]]
> [!code] [[screen]] #command
> با این دستور میتوانیم اسکرین های مختلفی ایجاد و مدیریت کنیم، و با قطع شدن ssh یا ترمینال نگران پردازش های در حال اجرا نباشیم.

> [!search] در صورت نیاز، آپشن های screen را در کتاب برای امتحان مطالعه کنید. 

#### TMUX
[[tmux]] نرم افزار جدیدتری است که امکانات بیشتری نسبت به اسکرین دارد.
هر session تیماکس میتواند چندین پنجره bash داشته باشد
تیماکس دستورات گسترده ای دارد. به عنوان مثال دو نفر با استفاده از یک یوزر میتوانند یک صفحه تیماکس را ببینند و روی آن کار کنند.