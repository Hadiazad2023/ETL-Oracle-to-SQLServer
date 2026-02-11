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
