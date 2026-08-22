# حل غرفة Fools Mate

> **الحالة:** مكتملة رسمياً داخل TryHackMe؛ تم قبول العلم وظهرت صفحة **Great work 9gkc! Room completed!**.

## معلومات الغرفة

| البيان | القيمة |
|---|---|
| اسم الغرفة | Fools Mate |
| الرابط الرسمي | [TryHackMe — Fools Mate][3] |
| الوصف | Can you bypass the engine? |
| الصعوبة | Easy |
| المدة المقدرة | 15 دقيقة |
| عنوان جهاز المختبر | `10.48.150.166` |
| التطبيق | `http://10.48.150.166` |
| المهمة | Task 1 — What is the flag? |
| النتيجة | **Correct Answer** ثم **Room completed** |
| النقاط | 30 |

## الإجابة المؤكدة

| المهمة | السؤال | الإجابة | التحقق |
|---|---|---|---|
| Task 1 | What is the flag? | `THM{cl13nt_s1d3_ch3ckm4t3}` | **Correct Answer** داخل TryHackMe ثم صفحة الإكمال الرسمية |

## تحليل المشكلة

تعرض الغرفة لوحة شطرنج يكون فيها الرخ الأبيض على `a1`، وتكون النقلة `a1` إلى `a8` هي كش ملك. عند محاولة تنفيذ النقلة من الواجهة، تمنعها الصفحة وتعرض رسالة تحذيرية. هذا السلوك الفوري يشير إلى أن المنع يحدث قبل إرسال الطلب إلى الخادم.[1] [2]

بفحص مصدر الصفحة وملف `js/app.js`، يظهر فحص محلي شبيه بما يلي:

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

تتحقق الدالة من كش الملك على نسخة محلية من حالة اللعبة، ثم تمنع استدعاء الشبكة إذا كانت النقلة تؤدي إلى كش ملك. لكن هذا ليس ضابطاً أمنياً حقيقياً، لأن المستخدم يستطيع إرسال الطلب مباشرةً دون المرور بهذا الفحص.[2]

## تجاوز التحقق من جهة العميل

يعتمد التطبيق على endpoint خلفي لمعالجة النقل:

```text
POST /api/move
Content-Type: application/json
```

تُرسل النقلة الفائزة مباشرةً إلى الخادم باستخدام:

```bash
curl -s -X POST http://10.48.150.166/api/move \
  -H 'Content-Type: application/json' \
  -d '{"from":"a1","to":"a8"}'
```

بهذا الأسلوب لا تُستدعى دالة `preMoveCheck` الموجودة في المتصفح، ويعالج الخادم النقلة. ويمكن تنفيذ الفكرة نفسها باعتراض طلب شرعي وتعديله في Burp Repeater أو بتعطيل JavaScript، لكن الطلب المباشر يوضح جوهر الثغرة.[1]

## العلم النهائي

```text
THM{cl13nt_s1d3_ch3ckm4t3}
```

## التحقق داخل TryHackMe

تم إدخال العلم في حقل Task 1 والضغط على **Check**. بعد اكتمال التحقق، انتقلت المنصة إلى صفحة التهنئة الرسمية وظهرت الرسالة:

> **Great work 9gkc! Room completed!**

وأظهرت الصفحة إكمال مهمة واحدة والحصول على **30 نقطة**؛ لذلك تم التحقق من الإجابة رسمياً داخل TryHackMe.

## الدرس الأمني

توضح الغرفة خطورة الاعتماد على التحقق من جهة العميل لفرض قواعد اللعبة أو منطق الأعمال. يمكن للمستخدم التحكم في JavaScript أو تجاوزه أو إعادة بناء طلب HTTP يدوياً. يجب أن يطبق الخادم التحقق من قانونية النقلة، وحالة اللوحة، ونتيجة كش الملك قبل تعديل الحالة أو إصدار العلم.

## المراجع

[1]: https://0xb0b.gitbook.io/writeups/tryhackme/2026/fools-mate "0xb0b — Fools Mate Write-up"

[2]: https://medium.com/@sudoroot523/tryhackme-fools-mate-fe3bb06eb89d "Sudoroot — TryHackMe: Fool’s Mate"

[3]: https://tryhackme.com/room/foolsmate "TryHackMe — Fools Mate"

---

إعداد: **Manus AI**

إطار الاستخدام: جميع الخطوات ضمن مختبر TryHackMe المصرح به ولأغراض تعليمية ودفاعية.

