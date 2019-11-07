# Malware Analysis Report (Azaza-SBB)
<div dir="rtl" align="right" >
    <p>
        فایل اکسلی با مشخصات زیر تحت عنوان فایل آلوده جهت بررسی ارجاع داده شده است :
    </p>
</div>

- Filename : sbb.xslx
- Filesize : 28,170 bytes
- Modification & Creation Time : August ‎4, ‎2016, ‏‎6:43:48 PM
- MD5 : dab5b6db23d73c63fe867ed4f801baea

<div dir="rtl" align="right" >
    <p>
        پس بررسی های اولیه مشخص شد فایل مورد نظر Obfuscate شده است و شخصی با نام احتمالی Azaza بر اساس دیتای موجود در فایل این فایل را ایجاد کرده است.
    </p>
</div>

```
C:\DOCUME~1\azaza\0016~1\out(5)\SBB_CH~1.JS
```
<div dir="rtl" align="right" >
    <p>
        جهت بررسی بیشتر فایل بد افزار موجود از طریق بررسی خط به خط کد های آن مجددآ بازنویسی شد که فایل malware_prettified.js به پیوست موجود می باشد.
    </p>
</div>

<div dir="rtl" align="right" >
    <p>
        بد افزار مورد نظر دارای ۴ پروکسی سرور می باشد که در پشت شبکه TOR پنهان شده است و از طریق Entrypoint های Onion.to و Onion.link تلاش می کند ترافیک مرورگر های فایرفاکس و کروم و اینترنت اکسپلورر قربانی را به صورت رندوم به سمت پروکسی سرور های زیر هدایت کند.
    </p>
</div>

- j65je6flfiejsea2.onion
- srj6jqfnn4eobrgn.onion
- zgu5v7fzwito746r.onion
- mvbcmt5ao7vdbprh.onion


<div dir="rtl" align="right" >
    <p>
        در بخشی از کد مخرب درخواست هایی برای سایت های زیر جهت شناسایی آیپی پابلیک کاربر و همچنین بررسی اتصال اینترنتی انجام می دهد.
    </p>
</div>

- api.ipify.org
- icanhazip.com

<div dir="rtl" align="right" >
    <p>
        پروکسی سرور و Endpoint مربوط به هر کاربر به صورت رندوم ساخته می شود و نمونه ای از Endpoint مورد نظر جهت آشنایی با ساختار آن در زیر ذکر شده است.
    </p>
</div>

```
https://j65je6flfiejsea2.onion.to/asd23s42.js?ip=1.1.1.1
```

<div dir="rtl" align="right" >
    <p>
        همچنین نفوذگر برای فراهم کردن امکان رمزگشایی از ترافیک HTTPS ارسالی و دریافتی کاربر گواهینامه ای جعلی با نام شرکت Comodo را از طریق پاورشل در لیست گواهینامه های مورد اعتماد مرورگر های کاربر اضافه می کند.
    </p>
</div>

# Analysis Instructions
<div dir="rtl" align="right" >
    <p>
        ابتدا آبجکت های درون فایل اکسل مشکوک را توسط دستور زیر لیست می کنیم و موارد مشکوک را خروجی می گیریم.
    </p>
</div>

```bash
zipdump.py -e sbb.xlsx
```

<div dir="rtl" align="right" >
    <p>
        لازم است باید تک تک ابجکت های مشکوک بررسی گردد اما دراین مورد با استفاده از Signature های موجود, شناسه ابجکت آلوده احتمالی توسط دستورات زیر استخراج شد.
    </p>
</div>

```bash
zipdump.py -y maldoc.yara -C decoder_xor1,decoder_rol1,decoder_add1 sbb.xlsx
```

<div dir="rtl" align="right" >
    <p>
در مورد فوق امضای maldoc_OLE_file_magic_number در ابجکت شماره ۱۰ یافت شد که نیاز به بررسی بیشتر دارد و از طریق دستور زیر ابجکت مورد نظر را در یک فایل خروجی می گیریم.
    </p>
</div>

```bash
zipdump.py -s 10 -d sbb.xlsx > malware_obfuscated.object
```

<div dir="rtl" align="right" >
    <p>
        با توجه بررسی ها فایل خروجی داده شده دارای هدر هایی می باشد که باید از بخش اجرایی جاوااسکریپت موجود جدا شود در نتیجه تا قبل از دستور eval همه موارد حذف می شود.
    </p>
    <p>
        سپس محتوای جدید در فایل malware_obfuscated.js ذخیره می شود, دلیل این نام گذاری پیرو مشاهده نشانه هایی از obfuscation در خروجی می باشد.
    </p>
    <p>
        سپس فایل obfuscate شده را توسط ابزار box-js بوسیله دستورات زیر تا حد امکان deobfuscate می کنیم و خروجی ایجاد شده در فولدر همنام فایل را جهت یافت بد افزار بررسی می کنیم.
    </p>
</div>
