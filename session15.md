#### first 45 min:
در کد بود\
درس تئوری داده نشد\
اتصال برنامه به منگو دیبی\
تغییرات در کد بخش\
Rule, specification\
کار با robo3\

---

put in rest api ==> to replace a document entirely
patch in rest api ==> for partial update


نکته مهم:

```text
## نکته‌ای در طراحی REST API: تفاوت PUT، PATCH و RPC

### ۱. تفاوت PUT و PATCH

- **PUT:** برای جایگزینی کامل یک Resource با نمایش جدید آن استفاده می‌شود.
- **PATCH:** برای اعمال تغییرات جزئی روی یک Resource استفاده می‌شود؛ مثلاً تغییر مقدار یک فیلد بدون ارسال مجدد تمام فیلدها.

**مثال:** فرض کنید می‌خواهیم یک Rule را فعال یا غیرفعال کنیم و فقط فیلد `isActive` تغییر کند.

```http
PATCH /rules/123
Content-Type: application/merge-patch+json
```

```json
{
  "isActive": false
}
```

در این درخواست، فقط وضعیت فعال بودن Rule تغییر می‌کند و سایر فیلدها دست‌نخورده باقی می‌مانند.

### ۲. تفاوت طراحی Resource-oriented با RPC-style

**طراحی مبتنی بر Resource (سبک REST):**

```http
PATCH /rules/123
```

```json
{
  "isActive": true
}
```

در این روش، با استفاده از متد HTTP و ارسال تغییرات در Body، وضعیت یک Resource را تغییر می‌دهیم.

**طراحی مبتنی بر عملیات (RPC-style):**

```http
POST /rules/123/activate
```

در این روش، به‌جای تغییر مستقیم یک ویژگی از Resource، یک عملیات مشخص به نام `activate` را فراخوانی می‌کنیم.

در نتیجه، استفاده از نام فعل‌هایی مانند `activate`، `deactivate` یا `approve` در مسیر API می‌تواند نشان‌دهندهٔ طراحی Action-oriented یا RPC-style باشد.

### ۳. آیا استفاده از endpointهای عملیاتی اشتباه است؟

خیر. RPC-style ذاتاً اشتباه نیست؛ انتخاب آن به ماهیت عملیات و قرارداد API بستگی دارد.

- اگر فعال یا غیرفعال بودن صرفاً یک ویژگی قابل‌ویرایش باشد، `PATCH /rules/{id}` انتخاب مناسبی است.
- اگر فعال‌سازی یک عملیات مستقل در دامنه باشد و نیازمند اعتبارسنجی‌ها یا قواعد خاصی باشد، endpoint عملیاتی مانند `POST /rules/{id}/activate` نیز می‌تواند انتخاب معتبری باشد.

### ۴. ارتباط با DDD

در DDD، تغییر یک فیلد نباید باعث دور زدن قواعد دامنه (Domain Invariants) شود. چه از PATCH استفاده کنیم و چه از یک endpoint عملیاتی، منطق فعال‌سازی و اعتبارسنجی قوانین دامنه باید در لایهٔ مناسب اجرا شود.

**نکتهٔ کلیدی:** انتخاب HTTP Method و طراحی endpoint باید بر اساس معنای عملیات و مدل Resource انجام شود، نه صرفاً سلیقهٔ برنامه‌نویس.

**منابع مطالعه:**
- RFC 5789 — PATCH Method for HTTP
- *The Design of Web APIs* — Arnaud Lauret
- *API Design Patterns* — JJ Geewax
```

---

### Task based UI or Inductice User Interface

بحث مهمی است
بر اساس نباز کاربر و فلویی که کاربر در سیستم دارد 
طراحی فرانت و بکند انجام میشود و
همه چیز از روز اول کراد در نظر گرفته نشود

خیلی تاکید کردند که نباید همه چیز را در سیستم کراد دید
باید به فلو و جرنی که کاربر در سیستم باید طی کند توجه کرد
و براساس آن سیستم دیزاین شود

یک کتاب از مایکروسافت معرفی کردند به نام
Exploring CQRS and Event Sourcing (from microsoft)


کتاب هایی که در این جلسه معرفی شد
- REST API design rulebook
- Exploring CQRS and Event Sourcing (from microsoft)
- Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 3rd Edition
by Krzysztof Cwalina, Jeremy Barton, Brad Abrams

