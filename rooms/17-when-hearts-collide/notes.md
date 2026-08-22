# ملاحظات غرفة When Hearts Collide — TryHackMe

## معلومات الغرفة

- **اسم الغرفة:** When Hearts Collide
- **الفعالية:** Love at First Breach 2026
- **الرابط:** https://tryhackme.com/room/lafb2026e1
- **التصنيف:** Web
- **الصعوبة:** Medium
- **المختبر:** `whenheartscollide_v1.1`
- **عنوان المختبر المؤقت:** `10.48.190.152`
- **المهام:** مهمة واحدة

## فكرة التحدي

يعرض التطبيق خدمة Matchmaker التي تقارن قيمة MD5 للصورة المرفوعة مع قيم MD5 لصور كلاب محفوظة في قاعدة البيانات. الهدف هو الوصول إلى صورة تطابق قيمة MD5 الموجودة في قائمة الصور، ثم الحصول على العلم من نتيجة المطابقة.

## مسار الحل

توضح صفحة الغرفة أن التطبيق يطلب رفع صورة، ثم يحسب MD5 للملف ويبحث عن تطابق. يكشف فحص التطبيق ومسار الحل أن صورة كلب مرجعية موجودة تحت المسار:

```text
/static/uploads/00795a8b-fb58-47c0-91be-af068ddc71b4.jpg
```

المشكلة الأمنية هي الاعتماد على **MD5** للمطابقة. وبما أن MD5 غير مناسب كآلية أمان، يمكن استخدام أداة collision مثل `fastcoll` لإنشاء ملفين مختلفين لهما قيمة MD5 متطابقة مع الصورة المرجعية. بعد رفع أحد ملفات التصادم، يعتبر التطبيق الملف صورة الكلب المطابقة ويعرض العلم.

## الإجابة المتحققة

العلم الذي قبلته TryHackMe هو:

```text
THM{hash_puppies_4_all}
```

## دليل التحقق داخل المنصة

تم إدخال العلم في حقل السؤال والضغط على **Check**. ظهرت عبارة **Correct Answer**، ثم انتقلت الغرفة إلى صفحة التهنئة التي عرضت **Room completed: 100%** و**Completed tasks: 1** و**Points earned: 200**.

لم يتم إرسال تقييم الغرفة أو الضغط على **Submit now**، التزاماً بتفضيل المستخدم.

## الدروس الأمنية

لا ينبغي استخدام MD5 لمطابقة الملفات في سياق أمني أو لاتخاذ قرار ثقة. ينبغي استخدام SHA-256 أو SHA-3، والتحقق من محتوى الملف وتوقيعه أو بصمته الآمنة، وعدم اعتبار تطابق MD5 دليلاً على أن الملف هو الملف الأصلي.

## مراجع العمل

1. [TryHackMe — When Hearts Collide](https://tryhackme.com/room/lafb2026e1)
2. [N3k0sint — When Hearts Collide Walkthrough](https://medium.com/@N3k0sint/love-at-first-breach-2026-tryhackme-when-hearts-collide-walkthrough-ctf-bd126374983f)
3. [RFC 6151 — Updated Security Considerations for the MD5 Message-Digest Algorithm](https://www.rfc-editor.org/rfc/rfc6151)
