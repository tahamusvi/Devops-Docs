

tman@pg:/bin$ readelf -h /bin/ls
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              DYN (Position-Independent Executable file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x6d30
  Start of program headers:          64 (bytes into file)
  Start of section headers:          140328 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           56 (bytes)
  Number of program headers:         13
  Size of section headers:           64 (bytes)
  Number of section headers:         31
  Section header string table index: 30

مجیک نشون دهنده اینه که فایل از چه نوعی هستش

| نوع فایل | Magic Number (در هگز) | معنی                                         |
| -------- | --------------------- | -------------------------------------------- |
| فایل ELF | `7f 45 4c 46`         | یعنی فایل اجرایی یا لینک‌شونده مخصوص لینوکسه |
| فایل PNG | `89 50 4E 47`         | یعنی فایل تصویری PNG                         |
| فایل ZIP | `50 4B 03 04`         | یعنی فایل zip                                |
| فایل PDF | `25 50 44 46`         | یعنی فایل PDF (`%PDF`)                       |

فیلد بعدی یعنی کلاس میگه برای چه پردازنده ای قابل اجرا هستش.

فیلد بعدیش میگه چطوری دیتاها ذخیره شدن 


ABI : Application Binary Interface

فیلد بعدی یعنی تایپ نوع فایل ELF رو نشون میده:

|مقدار|معنی|
|---|---|
|`EXEC`|فایل اجرایی عادی (قدیمی‌تر)|
|`DYN`|**Position Independent Executable** (PIE) یا shared object|
|`REL`|فایل relocatable (مثل object file در هنگام کامپایل)|
|`CORE`|فایل core dump بعد از crash برنامه|


#### Entry point address
  این آدرسه به سیستم‌عامل می‌گه:
> «بعد از اینکه همه‌چیز لود شد، اجرای برنامه رو از این نقطه (آدرس) شروع کن.»



#### `Start of program headers: 64 (bytes into file)`

یعنی جدول Program Header از بایت شماره ۶۴ در فایل شروع می‌شه


#### `Number of program headers: 13`

این یعنی ۱۳ تا برنامه یا بخش قابل بارگذاری (segment) توی این فایل تعریف شده.


#### `Start of section headers: 140328 (bytes into file)`

این می‌گه جدول سکشن‌ها (Section Headers) از بایت ۱۴۰۳۲۸ شروع می‌شه.



#### `Number of section headers: 31`

یعنی فایل `ls` شامل ۳۱ سکشن مختلفه.


|نام|کاربرد|
|---|---|
|`.text`|کد اجرایی برنامه|
|`.data`|داده‌های قابل نوشتن|
|`.rodata`|داده‌های فقط‌خواندنی|
|`.bss`|متغیرهای بدون مقدار اولیه|
|`.dynsym`, `.dynstr`|جدول سمبل‌های داینامیک|
|`.debug*`|برای دیباگ (در فایل‌های non-stripped)|


#### `Section header string table index: 30`

آخرین سکشن (شماره ۳۰) یک string table هست که اسم بقیه سکشن‌ها رو در خودش داره.  
بقیه سکشن‌ها با offset به این string table اشاره می‌کنن تا اسم خودشون رو بدونن.