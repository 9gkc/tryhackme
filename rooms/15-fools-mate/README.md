# Fools Mate — TryHackMe

> **الحالة:** مكتملة رسمياً داخل TryHackMe؛ تم قبول العلم وظهرت صفحة `Great work 9gkc! Room completed!`. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط الرسمي | [TryHackMe — Fools Mate][1] |
| الوصف | `Can you bypass the engine?` |
| التصنيف | Web / Client-side validation |
| الصعوبة | Easy |
| مدة المختبر | 15 دقيقة |
| عنوان المختبر | `10.48.150.166` |
| التطبيق | `http://10.48.150.166` |
| المهمة | Task 1 — What is the flag? |

## الملخص التنفيذي

تعرض الغرفة تطبيق شطرنج على الويب تكون فيه النقلة من `a1` إلى `a8` كش ملك. تمنع واجهة المستخدم هذه النقلة قبل إرسالها إلى الخادم بواسطة فحص JavaScript محلي، لكن الخادم لا يطبق الفحص نفسه على الطلب الوارد. لذلك يكمن جوهر الحل في تجاوز التحقق من جهة العميل وإرسال النقلة مباشرة إلى endpoint الخلفي داخل المختبر.[1]

## مسار الحل

### 1. تحديد النقلة ونقطة المنع

تبدأ حالة اللوحة بالرخ الأبيض على `a1`، وتؤدي النقلة إلى `a8` إلى كش ملك. عند تنفيذها من الواجهة تظهر رسالة تحذير، ما يشير إلى أن المنع يحدث في المتصفح قبل الوصول إلى الخادم.

يكشف فحص ملف `js/app.js` دالة محلية شبيهة بالتالي:

```javascript
function preMoveCheck(from, to, promotion) {
  const probe = new Chess(game.fen());
  let result;
  try {
    result = probe.move({ from, to, promotion: promotion || undefined });
  } catch (e) {
    result = null;
  }
  if (result && probe.isCheckmate()) {
    showSystemNotice("I'll shut down your PC if you play that.");
    return false;
  }
  return true;
}
```

المهم أمنياً أن هذه الدالة جزء من كود العميل وليست ضابطاً على الخادم؛ يمكن تجاوزها أو إعادة بناء الطلب من خارج الواجهة.[2]

### 2. تجاوز التحقق من جهة العميل

يعالج الخادم النقل عبر endpoint التالي:

```text
POST /api/move
Content-Type: application/json
```

تُرسل النقلة مباشرةً باستخدام `curl`:

```bash
curl -s -X POST http://10.48.150.166/api/move \
  -H 'Content-Type: application/json' \
  -d '{"from":"a1","to":"a8"}'
```

يؤدي هذا الطلب إلى تجاوز `preMoveCheck` الموجود في المتصفح، مع إبقاء التنفيذ ضمن نطاق مختبر TryHackMe المصرح به.

### 3. استخراج العلم

أعاد الخادم نتيجة النقلة الفائزة متضمنة العلم التالي:

```text
THM{cl13nt_s1d3_ch3ckm4t3}
```

## الإجابات النهائية

| المهمة | السؤال | الإجابة المقبولة |
|---|---|---|
| Task 1 | What is the flag? | `THM{cl13nt_s1d3_ch3ckm4t3}` |

## التحقق الرسمي داخل TryHackMe

أُدخل العلم في حقل Task 1 ثم تم الضغط على **Check**. ظهرت عبارة **Correct Answer**، ثم صفحة الإكمال الرسمية:

> **Great work 9gkc! Room completed!**

كما أظهرت الصفحة إكمال مهمة واحدة والحصول على 30 نقطة. لم يُرسل تقييم الغرفة ولم يتم الضغط على **Submit now**.

## الدروس الأمنية

لا يجوز استخدام JavaScript في المتصفح لفرض قواعد أمنية أو منطق أعمال حاسم؛ يستطيع المستخدم التحكم في الكود وإعادة بناء طلب HTTP يدوياً. يجب أن يتحقق الخادم من قانونية النقلة وحالة اللوحة ونتيجة كش الملك قبل تغيير الحالة أو إصدار أي مكافأة.

## المراجع

[1]: https://tryhackme.com/room/foolsmate "TryHackMe — Fools Mate"
[2]: https://0xb0b.gitbook.io/writeups/tryhackme/2026/fools-mate "0xb0b — Fools Mate Write-up"
