## مرحله 1: ساخت کلید خصوصی و CSR
```bash
openssl genrsa -out client.key 2048
```
```bash
openssl req -new -key client.key -out client.csr \
  -subj "/C=IR/ST=Tehran/O=MyOrg/OU=IT/CN=myclient"
```

## مرحله 2: ارسال فایل .csr به CA
فایل client.csr رو به شخص یا سازمان CA بده (مثلاً با ایمیل یا secure upload).

اون فرد/سازمان فایل رو با CA خودش امضا می‌کنه و بهت برمی‌گردونه.


## مرحله 3: دریافت گواهی امضا شده از CA
فرض کنیم گواهی برگشتی اسمش هست client.crt

## مرحله 4: بررسی صحت گواهی امضا شده
اگر اون‌ها یک CA عمومی دارن (مثلاً ca.pem)، با این دستور اعتبار رو بررسی کن:
```bash
openssl verify -CAfile ca.pem client.crt
```

 خروجی باید باشه:

```bash
 client.crt: OK
```
