# ملاحظات غرفة Fools Mate

## بيانات الغرفة

- **اسم الغرفة:** Fools Mate
- **الرابط:** https://tryhackme.com/room/foolsmate
- **الوصف:** Can you bypass the engine?
- **الصعوبة:** Easy
- **المدة المقدرة:** 15 دقيقة
- **عنوان جهاز المختبر:** `10.48.150.166`
- **الخدمة:** تطبيق شطرنج عبر HTTP على `http://10.48.150.166`
- **المهمة:** Task 1 — What is the flag?
- **الحالة النهائية:** مكتملة رسمياً؛ ظهرت صفحة `Great work 9gkc! Room completed!`، مع إكمال مهمة واحدة والحصول على 30 نقطة.

## الفكرة الأساسية

تظهر لوحة الشطرنج أن النقلة الرابحة هي نقل الرخ من `a1` إلى `a8`. تحاول واجهة التطبيق منع النقلة لأنها تؤدي إلى كش ملك، لكن المنع يتم بواسطة JavaScript في المتصفح فقط. لا يطبق الخادم فحصاً مطابقاً عند استقبال الطلب، ولذلك يمكن تجاوز المنع بإرسال طلب HTTP مباشر إلى endpoint الحركة.[1] [2]

## خطوات الاستغلال

1. فتح التطبيق من جهاز المختبر.
2. ملاحظة أن محاولة النقلة `a1` إلى `a8` من الواجهة تُمنع محلياً.
3. فحص ملفات JavaScript، خصوصاً `js/app.js`، وملاحظة دالة `preMoveCheck` التي تحاكي النقلة وتمنعها إذا اكتشفت `checkmate`.
4. تحديد endpoint الخادم:

```text
POST /api/move
Content-Type: application/json
```

5. إرسال النقلة الفائزة مباشرةً إلى الخادم، متجاوزاً فحص JavaScript:

```bash
curl -s -X POST http://10.48.150.166/api/move \
  -H 'Content-Type: application/json' \
  -d '{"from":"a1","to":"a8"}'
```

يمكن أيضاً تنفيذها عبر Burp Repeater أو تعطيل JavaScript، لكن الطلب المباشر يوضح أن المشكلة في الاعتماد على التحقق من جهة العميل فقط.[1]

## العلم المؤكد

```text
THM{cl13nt_s1d3_ch3ckm4t3}
```

تم إدخال العلم في TryHackMe ثم الضغط على **Check**. ظهرت صفحة الإكمال الرسمية، ما يؤكد قبول الإجابة.

## الدرس الأمني

لا يجوز استخدام JavaScript في المتصفح لفرض قواعد أمنية أو منطق أعمال حاسم؛ يستطيع المستخدم تجاوز هذا المنطق بإيقاف JavaScript أو إعادة بناء الطلب يدوياً. يجب على الخادم التحقق من صحة النقل وحالة اللعبة وقواعد كش الملك قبل تغيير الحالة أو إصدار أي مكافأة.

## المراجع

[1]: https://0xb0b.gitbook.io/writeups/tryhackme/2026/fools-mate "0xb0b — Fools Mate Write-up"

[2]: https://medium.com/@sudoroot523/tryhackme-fools-mate-fe3bb06eb89d "Sudoroot — TryHackMe: Fool’s Mate"

[3]: https://tryhackme.com/room/foolsmate "TryHackMe — Fools Mate"

---

إعداد: **Manus AI**

إطار الاستخدام: مختبر TryHackMe مصرح به وتعليمي.

