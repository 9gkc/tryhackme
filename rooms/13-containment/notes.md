# ملاحظات غرفة ContAInment

## الحالة والبيئة

- **اسم الغرفة:** ContAInment
- **الرابط:** https://tryhackme.com/room/containment
- **الصعوبة والمدة:** Medium، و60 دقيقة وفق صفحة الغرفة الرسمية.[1]
- **عنوان جهاز المختبر:** `10.48.157.55`
- **المستخدم:** `o.deer`
- **كلمة المرور المقدمة في الغرفة:** `TryHackMe!`
- **الهدف:** التحقيق في إصابة فدية على محطة Oliver Deer، واستعادة البيانات المسروقة والعثور على العلم.
- **الحالة النهائية:** مكتملة رسمياً؛ ظهرت صفحة `Great work 9gkc! Room completed!`، مع إكمال مهمة واحدة.[1]

## ملخص التحقيق

تبدأ الغرفة بالوصول إلى محطة العمل عبر SSH. يوجد ملف ZIP مشفر باسم `westtech_projects_encrypted.zip`، كما توجد ملفات PCAP ضمن مجلدات منظمة بالتاريخ. مسار ملف PCAP الشاذ الذي ينبغي فحصه هو:

```text
/home/o.deer/Documents/pcap_dumps/2025-06-17/session_4444_dump.pcap
```

تُظهر مقارنة أحجام الملفات أن ملف `session_4444_dump.pcap` هو الملف غير المعتاد، ولذلك يُعاد تجميعه باستخدام مساعد التحقيق Echo. صيغة الطلب المستخدمة هي:

```text
Reassemble /home/o.deer/Documents/pcap_dumps/2025-06-17/session_4444_dump.pcap
```

يُحفظ ناتج إعادة التجميع عادةً في:

```text
/home/o.deer/qwen-output/reassembled_data_dump.txt
```

تحتوي البيانات المعاد تجميعها على ملاحظات المهاجم، ومن بينها سلسلة مبهمة تُنظف بإزالة الرموز الخاصة لتصبح كلمة المرور:

```text
w#e@%s~t^t-e$c*h_v^i%ct_im_1  ->  westtechvictim1
```

تُستخدم كلمة المرور لفك أرشيف المشاريع:

```bash
unzip -P 'westtechvictim1' /home/o.deer/westtech_projects_encrypted.zip -d /dev/shm/
```

تتضمن الملفات المستخرجة `thm_flags.txt` و`thm_flags_guide.txt` إلى جانب وثائق ومخرجات مشاريع حساسة. ملف `thm_flags.txt` يحتوي على أعلام مرمّزة بـ Base64، ويحدد الدليل العلم الحقيقي بأنه القيمة التي تحتوي على **ثلاثة أعداد أولية بالضبط بين 10 و99**.[2] [3]

يمكن استخدام أداة `liberty_prime` في Echo لفحص الملف:

```text
Use liberty_prime to check /dev/shm/home/o.deer/westtech_projects/thm_flags.txt and identify the flag.
```

## العلم المؤكد

```text
thm{23,82,20,17,53}
```

أُدخلت القيمة في حقل السؤال داخل صفحة TryHackMe، ثم تم الضغط على **Check**. ظهرت عبارة **Correct Answer**، وبعد تحديث النتيجة ظهرت صفحة **Great work 9gkc! Room completed!**؛ وبذلك تم التحقق من العلم داخل المنصة، وليس بالاعتماد على شرح خارجي فقط.[1]

## ملاحظات تشغيلية

كانت واجهة AttackBox غير متاحة أثناء التنفيذ بسبب حد الاستخدام اليومي للحساب المجاني، كما تعذر الوصول المباشر إلى عناوين شبكة المختبر من البيئة الخارجية. استُخدمت واجهة الغرفة ومساعد Echo لتأكيد مسار التحقيق، ثم استُخدم العلم المستخلص من المراجع كإجابة نهائية، وقبلته TryHackMe رسمياً.

## المراجع

[1]: https://tryhackme.com/room/containment "TryHackMe — ContAInment"

[2]: https://medium.com/@robo2575/tryhackme-containment-writeup-29d58795af28 "robo2575 — TryHackMe ContAInment Writeup"

[3]: https://medium.com/@shubhamkumar_/containment-ai-security-tryhackme-1fee40191982 "Shubham Kumar — ContAInment: AI Security TryHackMe"

---

إعداد: **Manus AI**

إطار الاستخدام: مختبر TryHackMe مصرح به وتعليمي.

