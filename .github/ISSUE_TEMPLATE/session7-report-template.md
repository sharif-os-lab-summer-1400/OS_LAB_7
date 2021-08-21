---
name: فرم گزارش آزمایش هفتم
about: برای نوشتن گزارش آزمایشگاه از این تمپلیت استفاده کنید
title: Session 7 Report
labels: documentation
assignees: alimirferdos

---

Team Name: 97110285-97101286

Student Name of member 1: Mohammadreza Abdi
Student No. of member 1: 97110285

Student Name of member 2: Alireza Ilami
Student No. of member 2: 97101286

- [ ] Read Session Contents.

## Section 7.4

### Section 7.4.1
- [X] Creating a thread using pthread
    - [X] ![image](https://user-images.githubusercontent.com/45389577/129480882-4e4bd976-4b9c-42c4-8216-624f40026349.png)
   
- [x]  Checking the process ids
    - [x] ![image](https://user-images.githubusercontent.com/45389577/129481687-1df31a0f-d1c3-49f1-80bd-324d1cff766c.png)
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130116244-b8ac26db-adb9-4f03-82d4-5fb2a8ea6919.png)
    - [x] در این برنامه در دو جای مختلف شماره پردازه را چاپ کردیم. در تابع ریسه، پردازه ریسه مورد نظر است و در تابع اصلی نیز ریسه اصلی. همانطور که مشاهده میشود، این دو عدد یکی هستند. یعنی یک پردازه لزوما شامل فقط یک ریسه نیست. بلکه میتواند شامل چند ریسه باشد. و همه این ریسه ها در پردازه وشماره آن با یکدیگر مشترک هستند.

- [x]  Shared variables
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130118300-8dccc29e-858b-4acb-b3cc-4a3a4085a2b4.png)
    - [x]  ![image](https://user-images.githubusercontent.com/45389577/130118411-44432458-ec6b-44a0-9398-98031185fe2d.png)
    - [x]  ما مقدار متغیر را در ریسه غیراصلی از 1 به 2 تغییر دادیم. و این نغییر در ریسه اصلی نیز لحاظ شد. و پس از ترد، در تابع اصلی نیز مقدار متغیر 2 است. و وقتی که ان را به 3 تغییر دهیم نیز به 3 تغییر میکند. این نشان میدهد که متغیرهای *سراسری* ربطی به ریسه ندارند و در کل پردازه یکسان هستند.

- [x] Sum of 2 to n
    1. [x] ![image](https://user-images.githubusercontent.com/45389577/130132126-cea418c7-f26b-4a25-9d14-25a1760c9c1e.png)
    1. [x] ![image](https://user-images.githubusercontent.com/45389577/130132320-6a588551-57c6-448b-87bb-8e4e3fca28db.png)

### Section 7.4.2
- [x] Multiple threads    
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130135177-4b3181d8-d683-4926-b0dc-20cce4cf61fb.png)
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130135269-303c86f7-a620-40d2-ab94-d5065d57ecee.png)

### Section 7.4.3
- [x] Compiling the code
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130323784-29c0a3ee-8e7a-4159-8647-c2ef38ede0ee.png)
    - [x] NOTE: Without defining the global_param as a global variable, the code could not be compiled successfully. 

- [x] global_param
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130324125-eaf171b3-089c-4e2b-82e9-fc7a4981d37d.png)
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130324137-f526af4d-8e52-4dd2-bfec-de4d55d0827b.png)

- [x] Forking
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130326461-e8e49180-f3d1-4bd0-aefa-90412c4ee0ab.png)
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130326484-7e45ef7e-7175-4835-9838-e34ace8b5ff9.png)
    - [x] مشاهده میکنیم که برای ریسه هایی که در یک پردازه قرار دارند، متغیرهای سراسری یکسان و متغیرهای محلی متفاوتند. اما برای ریسه های دو پردازه مختلف، هم متغیرهای سراسری و هم متغیرهای محلی متفاوتند. در تصویر مشاهده میشود که در دو خط آخر که چاپ شده، برای دو پردازه مختلف، متغیرها کاملا متفاوتند. ولو اینکه پردازه ها رابطه پدر و فرزندی داشته باشند و فورک کرده باشیم.
    
### Section 7.4.4
- [x] Passing multiple variables
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130328505-9bdf829b-456d-457e-b4da-0978f4e1c53c.png)
    - [x] ![image](https://user-images.githubusercontent.com/45389577/130328522-a9d301e0-c11a-4e38-9f79-b3dfe4f2219b.png)
