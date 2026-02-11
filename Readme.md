# پروژه ETL: انتقال داده از Oracle به SQL Server

## توضیح پروژه (فارسی)
این پروژه یک اسکریپت ETL است که داده‌ها را از دیتابیس Oracle می‌خواند و به SQL Server منتقل می‌کند.  
ویژگی‌های اصلی پروژه:
- انتقال امن و دقیق داده‌ها
- کنترل داده‌های تکراری بر اساس docSeq
- نمایش پروگرس بار برای عملیات
- ثبت گزارش خطا (Log)

---

## Project Description (English Summary)
This ETL project reads data from an Oracle database and inserts it into SQL Server.  
Key features:
- Safe and accurate data transfer
- Duplicate checking based on docSeq
- Progress bar to track ETL process
- Error logging

---

## مراحل اجرای پروژه (Step by Step)

### مرحله 1: تنظیم اتصال به دیتابیس‌ها
- اتصال به Oracle
- اتصال به SQL Server
```php
<?php
$ora_conn = oci_connect("username", "password", "localhost/XE");
$sql_conn = sqlsrv_connect("serverName", ["Database"=>"DB", "UID"=>"user", "PWD"=>"pass"]);
?>
مرحله 2: خواندن داده از Oracle

انتخاب داده‌های مورد نیاز

فیلتر داده‌های جدید بر اساس docSeq$sql = "SELECT * FROM source_table WHERE docSeq > :lastDocSeq";
مرحله 3: پردازش و تبدیل داده

تبدیل فرمت تاریخ‌ها

بررسی و اصلاح داده‌های ناقص

تبدیل کاراکترهای فارسی (در صورت نیاز)

مرحله 4: درج داده در SQL Server

استفاده از prepared statements برای جلوگیری از SQL Injection
$sql = "INSERT INTO Stage_FactExpense
(EXPENSEAMOUNT, ExpenceDesc, DateKey, RegionKey, BudgetKey, TypeId, docSeqn, CodeHesab)
VALUES (?, ?, ?, ?, ?, ?, ?, ?)";

مرحله 5: ثبت گزارش و پروگرس

نمایش درصد پیشرفت در ترمینال یا مرورگر

ذخیره log شامل خطاها و رکوردهای منتقل شده

مرحله 6: کنترل داده‌های تکراری

بررسی docSeq برای جلوگیری از درج مجدد داده‌ها

حذف رکوردهای ناقص یا تکراری
ETL-Oracle-to-SQLServer/
│
├─ scripts/         # اسکریپت‌های PHP و SQL
├─ docs/            # مستندات و تصاویر
├─ logs/            # فایل‌های گزارش
└─ README.md

نکات حرفه‌ای

قبل از اجرای ETL، آخرین docSeq درج شده در SQL Server را بررسی کنید.

برای داده‌های فارسی، encoding مناسب تنظیم شود (UTF-8 یا AR8MSWIN1256 برای Oracle).

commit های مرتب بزنید تا تغییرات و پیشرفت پروژه مشخص باشد.
License

این پروژه برای تمرین و نمونه کار شخصی است و رایگان است.
