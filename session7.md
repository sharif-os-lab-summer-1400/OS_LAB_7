<div dir="rtl" align='justify'>
   
# آزمایش ٧ - آشنایی با ریسه‌ها

## ۷.۱ مقدمه

هدف اصلی این آزمایش، بررسی جنبه های مختلف ریسه ها و چند پردازشی (و چند ریسه‌ای) است. از اهداف اصلی این آزمایش پیاده سازی توابع مدیریت ریسه ها است:

* ساخت ریسه ها
* پایان بخشیدن به اجرای ریسه
* پاس دادن متغير به ریسه ها
* شناسه های ریسه ها
* متصل شدن ریسه ها

### ۷.۱.۱ پیش‌نیازها

انتظار می‌رود که دانشجویان با موارد زیر از پیش آشنا باشند:

* برنامه نویسی به زبان C++/C

* دستورات پوسته لینوکس که در جلسات قبل فرا گرفته شدند.

## ۷.۲ ریسه چیست؟

یک ریسه، شبه پردازه ای است که پشته ی خاص خود را در اختيار دارد و کد مربوط به خود را اجرا می کند. برخلاف پردازه، یک ریسه، معمولا حافظه ی خود را با دیگر ریسه ها به اشتراک می گذارد. یک گروه از ریسه ها، یک مجموعه از ریسه ها است که در یک پردازه ی یکسان اجرا می شوند. بنابراین آنها یک حافظه ی یکسان را به اشتراک می گذارند و می توانند به متغیرهای عمومی یکسان، حافظه ی heap یکسان و ... دسترسی داشته باشند. همه ی ریسه ها می توانند به صورت موازی (استفاده از برش زمانی، یا اگر چندین پردازه وجود داشته باشد، به معنای واقعی موازی) اجرا شوند.

## ۷.۳ pthread

بر اساس تاریخ، سازندگان سخت افزار نسخه ی مناسبی از ریسه ها را براي خود پیاده سازی کردند. از آنجا که این پياده سازی ها با هم تفاوت می کرد، پس کار را برای برنامه نویسان، برای نگارش یک برنامه‌ی قابل حمل دشوار می کرد. بنابراین نياز به داشتن یک واسط یکسان برای بهره بردن از فواید ریسه‌ها احساس می شد. برای سيستم های Unix این واسط با نام IEEE POSIX ١٠٠٣ c.١ مشخص می شد و به پياده سازی مرتبط با آن POSIX THREADS یا pthread گفته می شود. اکثر سازندگان سخت افزار، علاوه بر نسخه ی مناسب با خودشان، استفاده از pthread را نيز پيشنهاد می کنند. pthread ها در یک کتابخانه ی C تعریف شده اند که شما می توانيد با برنامه ی خود link کنيد.

توابع موجود در این کتابخانه به صورت غیررسمی به سه دسته تقسيم می شوند:
*  مدیریت ریسه ها: دسته ی اول از این توابع به صورت مستقيم با ریسه ها کار می کنند. همانند ایجاد، متصل کردن و …
* Mutex: دسته ی دوم از این تابع برای کار با mutex ها ایجاد شده اند. توابع مربوط به mutex ابزار مناسب برای ایجاد، تخریب، قفل و بازکردن mutex ها را در اختيار قرار می دهند.
* متغیرهای شرطی (Conditional Variables): این دسته از توابع، براي کار با متغیرهای شرطی و استفاده از مفهوم همزمانی در سطح بالاتر در اختیار قرار می گیرند. این دسته از توابع براي ایجاد، تخریب، wait و signal بر اساس مقادیر معين متغيرها استفاده می شوند.

**نکته ۱**   در این جلسه قصد آن را داریم تا با دسته ی اول از توابع آشنا شویم. توابع مربوط به این دسته به طور خلاصه در جدول زیر مشاهده می شود: برای آشنایی با جزئيات می توانيد از دستور `man` و یا اینترنت استفاده کنيد.

  
<div align='center'>
  
  جدول ٧ .١ :توابع مربوط به مدیریت ریسه ها
  
| **نام تابع**                                                              |   **کاربرد**   |
|:-----------------------------------------------------------------------:|:----------------:|
| `pthread_create`   | از کتابخانه ی ،pthread درخواست ساخت یک ریسه ی جدید را می کند.           |
| `pthread_exit`     |  این تابع توسط ریسه استفاده شده تا پایان بپذیرد.                        |
| `pthread_join`     | این تابع، براي ریسه ی مشخص شده صبر می کند تا پایان بپذیرد.              |
| `pthread_cancel`   |  درخواست کنسل شدن ریسه ی مشخص شده را ارسال می کند.                      |
| `pthread_attr_int` |  مقدار attribute های پاس داده شده به خود را با مقادیر پیش فرض پر می کند. |
| `pthread_self`     |  شماره ی ریسه را بر می گرداند.                                          |
</div>


## ۷.۴ شرح آزمایش

### ۷.۴.۱ آشنایی اولیه

1. وارد سيستم عامل مجازی ایجاد شده در جلسات قبل شوید.

1. با استفاده از تکه کد زیر، یک ریسه ایجاد کنید.

<div dir="ltr">

```c
 #include<pthread.h>

int main() {
	pthread_t the_thread; 
	return 0;
}
```
</div>
دقت کنيد در هنگام کامپایل، lpthread -را به پرچم های linker اضافه كنيد:

<div dir="ltr">

```bash
gcc thread.c –o threads –lpthread
```
</div>

3. با استفاده از توابع pthread_create و pthread_join یک ریسه درست کنيد که در آن شماره ی پردازه را چاپ كنيد. همچنين در پردازه ی اصلی نيز شماره ی پردازه را چاپ كنيد. دقت کنيد پردازه ی اصلی بعد از پایان یافتن ریسه ها تمام شود. آیا شماره پردازه های چاپ شده یکسان می باشند؟

4. برنامه ی بالا را در یک فایل جدید کپی کنید. حال، متغير oslab را به این تکه کد به صورت عمومی اضافه كنيد. حال، یک بار این متغير را در ریسه ی اصلی و یک بار در ریسه ی فرزند تغيير دهيد. بعد از تغيير در ریسه ی فرزند، بار دیگر در ریسه ی اصلی چاپ كنيد. آیا ریسه ها کپی های جداگانه ای از متغير را دارند؟

5. با استفاده از تابع pthread_attr_int و تنظيم کردن attribute های ریسه به صورت پيش فرض، کدی بنویسید که در آن با گرفتن عدد n از ورودی، حاصل جمع اعداد ٢ تا n را چاپ کند.

### ۷.۴.۲ ريسه های چندتایی

در این قسمت قصد آن را داریم تا در یک کد، چند ریسه داشته باشيم.
* با استفاده از تابع، pthread_create تعدادي ریسه به تعداد دلخواه ایجاد کنيد (حداقل پنج تا) و پيام Hello World را در آن چاپ کنيد. سپس ریسه ها را با استفاده از تابع pthread_exit خاتمه دهيد. 

### ۷.۴.۳ تفاوت بين پردازه ها و ريسه ها

در این قسمت، قصد آن را داریم تا تفاوت ميان پردازه ها و ریسه ها را بهتر متوجه شویم.

1. تکه کد زیر را به عنوان تابع ریسه در فایلی بنویسید:

دقت کنيد در هنگام کامپایل، lpthread -را به پرچم های linker اضافه كنيد.

<div dir="ltr">

```c
void kid(void* param) {
	int local_param;
	printf("Thread %d, pid %d, addresses: &global: %X, &local: &X \n", 
	         pthread_self(), getpid(), &global_param , &local_param);
	global_param++;
	printf("In Thread %d, incremented global parameter=%d\n", 
	          pthread_self(), global_param);
	pthread_exit(0);
}
```
</div>

2. حال، در ریسه ی اصلی، یک متغیر عمومی به عنوان global_param تعریف کرده، مقداردهی کنيد و دو ریسه ی فرزند با تابع kid ایجاد و اجرا کنيد. در پایان ریسه ها نيز مقدار متغير global_param را چاپ كنيد.

3. حال، مقدار متغير عمومی را بار دیگر تغيير داده و یک متغير محلی دیگر در تابع اصلی تعریف کنید. آن را نيز مقدار دهی کنید. حال، با استفاده از تابع fork که در جلسات پيش یاد گرفته اید، یک پردازه ی فرزند ایجاد کرده و متغيرها را در آن دوباره مقدار دهی کنيد. تغييرات را با استفاده از تابع printf نمایش دهيد.

### ۷.۴.۴ پاس دادن متغیرها به ريسه‌ها
تابع pthread_create تنها اجازه می‌دهد که یک متغیر به عنوان ورودی به ریسه داده شود. براي حالاتی که چند پارامتر می بایست به ریسه داده شود، این محدودیت به راحتی با استفاده از ساختار (structure) حل می شود. تمامی متغيرها می بایست به وسيله ی reference و تبدیل به *void پاس داده شوند.

 ساختار زیر را در فایلی قرار دهيد:
<div dir="ltr">

```c
typedef struct thdata {
	int thread_no;
	char message[100];
} stdata;
```
</div>

حال، در ریسه‌ي اصلی، دو متغير از ساختار معرفی شده ایجاد کنید و مقادیر آن را به صورت دلخواه تنظيم کنيد. سپس، متغيرها را به دو ریسه‌ي جداگانه پاس بدهيد. در ریسه‌ها نيز عدد و پيام ذخيره شده در ساختار را نمایش بدهيد.
