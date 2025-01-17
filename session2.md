<div dir="rtl" align='justify'>

# آزمایش ٢ - آشنایی با فراخوانی های سیستمی


## ۲.۱ مقدمه
در این جلسه از آزمایشگاه با برخی از مهمترین فراخوانی‌های سیستمی در سیستم عامل لینوکس آشنا خواهیم شد و به کمک آنها چند برنامه خواهیم
نوشت. همچنین روش اضافه کردن فراخوانی‌های سیستمی به هسته لینوکس را خواهیم آموخت.

### ۲.۱.۱ اهداف
انتظار می‌رود در پایان این جلسه دانشجویان مطالب زیر را فرا گرفته باشند:

- آشنایی با مفهوم فراخوانی سیستمی.
- نحوه ی اجرای فراخوانی‌های سیستمی.
- فراخوانی‌های سیستمی مهم و پرکاربرد در سیستم‌عامل لینوکس.
- نحوه ایجاد فراخوانی‌های سیستمی جدید.

### ۲.۱.۲ پیش‌نیاز‌ها

انتظار می‌رود که دانشجویان با موارد زیر از پیش آشنا باشند:

-  برنامه‌نویسی به زبان ++c/c

## ۲.۲ فراخوانی سیستمی چیست؟
فراخوانی سیستمی یا system call تابعی است که در هسته‌ی سیستم‌عامل پیاده‌سازی شده است و هنگامی که یک برنامه یک فراخوانی سیستمی
انجام می‌دهد، کنترل اجرا از آن برنامه به هسته منتقل می‌شود تا عملیات درخواست شده صورت پذیرد. فراخوانی‌های سیستمی برای اعمال
مختلفی مانند دسترسی به منابع، تخصیص آنها، خاموش کردن یا راه‌اندازی مجدد سیستم‌عامل و ... مورد استفاده قرار می گیرد. برخی از این
فراخوانی های سیستمی تنها در پروسه‌هایی قابل استفاده است که توسط super-user اجرا شده باشند.


هر فراخوانی سیستمی با یک شماره ثابت شناخته می‌شود که این شماره پیش از کامپایل شدن هسته باید مشخص گردد. به همین دلیل در
سیستم‌عامل لینوکس افزودن فراخوانی‌های سیستمی تنها با کامپایل و نصب مجدد هسته امکان پذیر است.

برای اطلاعات بیشتر در مورد فراخوانی‌های سیستمی در لینوکس به  [اینجا](https://mentorembedded.github.io/advancedlinuxprogramming/alp-folder/alp-ch08-linux-system-calls.pdf) مراجعه کنید.

## ۲.۳ شرح آزمایش

### ۲.۳.۱ مشاهده فراخوانی‌های سیستمی تعریف شده

1. وارد سیستم‌عامل مجازی ایجاد شده در جلسه قبل شوید.

1. سیستم‌عامل لینوکس در حال حاضر شامل بیش از ٣٠٠ فراخوانی سیستمی است. فایل زیر را به کمک یک ویرایشگر باز کنید؛ در این
فایل می توانید لیست فراخوانی‌های سیستمی به همراه شماره‌ی آنها را بیابید.

<div dir="ltr">

```shell
/usr/include/i386-linux-gnu/asm/unistd_32.h
```


</div>


### ٢.٣.٢ اجرای یک فراخوانی سیستمی

1. در پوشه‌ی خانه خود یک فایل testsyscall.cpp ایجاد کنید.

1. کد زیر با استفاده از فراخوانی سیستمی mkdir یک پوشه جدید ایجاد می کند. آن را در فایلی که در مرحله قبل ایجاد کرده‌اید وارد کنید:
   
   برنامه نمونه برای ایجاد یک پوشه:
   <div dir="ltr">

    ```cpp
    #include <stdio.h>
    #include <unistd.h>
    #include <sys/syscall.h>
    int main () {
        long result;
        result = syscall(__NR_mkdir , "testdir", 0777);
        printf("The result is %ld.\n", result);
        return 0;
    }
    ```

    </div>

1. کد را کامپایل کنید و سپس اجرا نمایید.

1. نتیجه اجرای آن را شرح دهید.

1. در مثال بالا، نقش `__NR_mkdir` چیست؟
   
1. در مورد نحوه استفاده از دستور syscall و ورودی‌ها و خروجی‌های آن توضیح دهید.

### ۲.۳.۳ اجرای ساده‌تر فراخوانی سیستمی

برای کاربرد ساده‌تر فراخوانی‌های سیستم بدون نیاز به شماره آن‌ها، می توان از توابعی استفاده کرد که از پیش به عنوان wrapper برای آن ها نوشته
شده‌اند. برای مثال برای فراخوانی سیستمی بخش قبلی می توان از تابع ()mkdir که در `sys/stat.h` قرار دارد استفاده کرد. به دلیل خوانایی
بالاتر سادگی کاربرد، معمولا ترجیح بر استفاده از این توابع به جای استفاده مستقیم از دستور syscall است.

1. گد بخش قبل را به کمک تابع ()mkdir بازنویسی کنید و در فایل testsyscall2.cpp ذخیره نمایید.


### ۲.۳.۴ آشنایی با چند فراخوانی سیستمی پرکاربرد

در هر کدام از فعالیت‌های این بخش، یک فراخوانی سیستمی معروف می شود؛ به کمک این فراخوانی سیستمی برنامه‌های خواسته‌شده را بنویسید.
برای دریافت راهنمایی در مورد هر کدام از این فراخوانی‌های سیستمی می توانید از دستور `man 2 [syscall_name]` استفاده کنید.


- برای دیدن امکان دسترسی به فایل‌ها، فراخوانی سیستمی access مورد استفاده قرار می‌گیرد. برنامه‌ای بنویسید که به عنوان آرگومان
ورودی یک آدرس را دریافت کند و ببیند که آیا اولاً آن آدرس وجود دارد یا خیر و ثانیاً آیا دسترسی به آن برای پروسه‌ی اجرا شده امکان پذیر
است؟

- به کمک فراخوانی‌های سیستمی ،open close و write برنامه‌ای بنویسید که یک فایل با اسم oslab2.txt ایجاد کرده و نامتان را در آن
فایل بنویسد.

- به کمک فراخوانی سیستمی sysinfo برنامه‌ای بنویسید که میزان حافظه RAM کل و همچنین حافظه‌ی خالی را در خروجی چاپ کند.

- به کمک فراخوانی سیستمی getrusage برنامه‌ای بنویسید که میزان حافظه مصرفی خود را چاپ کند. 


### ۲.۳.۵ اضافه کردن یک فراخوانی سیستمی به سیستم‌عامل

همان طور که در ابتدا بیان شد، برای اضافه کردن فراخوان‌های سیستمی به هسته‌ی لینوکس نیازمند آن هستیم که هسته را مجدداً کامپایل و نصب
کنیم. برای اضافه کردن یک فراخوانی سیستمی سه گام اصلی باید انجام شود:

1. اضافه کردن تابع جدید،
2. به روزرسانی فایل‌های سرآیند،
3. به روزرسانی جدول فراخوانی‌های سیستمی.

در اینجا قصد داریم که یک فراخوانی سیستمی ساده را به سیستم‌عامل اضافه کنیم.

1. مطمئن شوید که با دسترسی root به سیستم‌عامل وارد شده اید.
2. وارد پوشه‌ی کد منبع هسته سیستم‌عامل که در جلسه قبل ایجاد کردیم شوید.
3. دستور make oldconfig را اجرا کنید. این دستور هسته‌ی جدید را مطابق با ویژگی های هسته‌ی فعلی که بر روی که بر روی سیستم
نصب شده است تنظیم می کند.
1. با دستور make هسته را کامپایل کنید و مطمئن شوید که این عملیات به درستی صورت می‌گیرد.
1. به کمک دستور make modules_install هسته‌ی جدید را نصب نمایید.
1. سیستم‌عامل را مجدداً راه‌اندازی کنید. دقت کنید که در منوی بوت، هسته جدید را انتخاب کنید.
1. یک پوشه خالی با نام hello در شاخه اصلی کد منبع هسته ایجاد کنید.
1. در این پوشه یک فایل hello.c شامل کد فراخوانی سیستمی با محتوای زیر ایجاد کنید:
    <div dir="ltr">

    ```cpp
    #include <linux/kernel.h>
    asmlinkage long sys_hello(void) {
        printk("Hello World\n");
        return 0;
    }
    ```

    </div>

1. یک فایل با نام Makefile در همین شاخه با محتوای زیر ایجاد کنید:
    <div dir="ltr">

    ```makefile
    obj-y := hello.o
    ```

    </div>

1. فایل Makefile موجود در ریشه‌ی کد منبع را باز کنید. در حوالی خط ٨٠٠ این فایل متنی مشابه زیر وجود دارد که به انتهای آن /hello
را اضافه نمایید.
    <div dir="ltr">

    ```makefile
    Core-y += kernrl/ mm/ fs/ ipc/ security/ crypto/ block/
    ```

    </div>

1. حال جداول مربوط به فراخوانی سیستمی را به روزرسانی می کنیم. فایل زیر را باز کرده و خط بلوک بعدی را در انتهای آن اضافه نمایید. 
آدرس فایل:
    <div dir="ltr">

    ```makefile
    ./arch/x86/syscalls/syscall\_ 32.tbl
    ```
    </div>
    
    خطی که باید اضافه کنید:
    <div dir="ltr">

    ```makefile
    357 i386 hello sys_hello
    ```
    </div>
    
1. در فایل زیر خطی به صورت بلوک بعدی اضافه کنید:
آدرس فایل:
    <div dir="ltr">

    ```bash
    ./include/linux/syscalls.h
    ```
    </div>


   خطی که باید اضافه کنید:
    <div dir="ltr">

    ```c
    asmlinkage long sys_hello(void);
    ```
    </div>

1. هسته را مجدداً کامپایل و نصب کنید و سیستم را دوباره راه‌اندازی نمایید.

#### کامپایل بر روی ورژن ۵ کرنل لینوکس

در صورتی که از ورژن‌های جدیدتر نسخه‌ی لینوکس استفاده می‌کنید کمی پروسه‌ی نوشتن کرنل ماژول متفاوت می‌تواند باشد.

در ابتدا محتوای فایل
hello.c
را به صورت زیر عوض کنید:
<div dir="ltr">

```cpp
#include <linux/kernel.h>
#include <linux/syscalls.h>

SYSCALL_DEFINE0(hello)
{
    printk("Hello World\n");
    return 0;
}
```
</div>

در نهایت در انتهای فایل
`arch/x86/entry/syscalls/syscall_64.tbl`
خط‌های زیر را اضافه کنید به جای خطی که در قسمت قبل ذکر شده بود.
<div dir="ltr">

```
441 common hello sys_hello
```
</div>

دقت کنید که 441 یک عدد ثابت نیست و باید با توجه به عدد آخرین
syscall
آنرا تنظیم کنید. حال می‌توانید کرنل لینوکس را کامپایل کنید و از
syscall
جدید خود استفاده کنید! برای اطلاعات بیشتر به
[این](https://armi3.hashnode.dev/how-to-add-a-custom-syscall-to-your-linux-kernel-581-in-ubuntu-2010-groovy-gorilla-ckmh27orq02j0kks123jg30a4) و [این](https://dev.to/jasper/adding-a-system-call-to-the-linux-kernel-5-8-1-in-ubuntu-20-04-lts-2ga8)
لینک می‌توانید مراجعه کنید.

حالا دو برنامه با کارکرد زیر بنویسید:

- برنامه‌ای بنویسید که از فراخوانی سیستمی hello استفاده کند. برای مشاهده‌ی خروجی چاپ شده آن از دستور dmesg استفاده کنید.
  
- یک فراخوانی سیستمی با نام adder بنویسید که دو عدد را با یکدیگر جمع کند.


برای اطلاعات بیشتر می‌توانید به [https://seshagiriprabhu.wordpress.com/2012/11/15/adding-a-simple-system-call-to-the-linux-3-2-0-kernel-from-scratch/](https://seshagiriprabhu.wordpress.com/2012/11/15/adding-a-simple-system-call-to-the-linux-3-2-0-kernel-from-scratch/) مراجعه کنید.

</div>
