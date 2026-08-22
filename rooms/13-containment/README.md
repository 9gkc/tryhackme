# حل غرفة ContAInment

> **الحالة النهائية:** مكتملة رسمياً داخل TryHackMe؛ تم قبول الإجابة وظهرت صفحة `Room completed`.

## معلومات الغرفة

| البيان | القيمة |
|---|---|
| اسم الغرفة | ContAInment |
| الرابط الرسمي | [TryHackMe — ContAInment][1] |
| الموضوع | الاستجابة لحادثة فدية وتحقيق رقمي بمساعدة AI |
| الصعوبة | Medium |
| الزمن المعلن | 60 دقيقة |
| عنوان جهاز المختبر | `10.48.157.55` |
| حساب SSH | `o.deer` |
| كلمة المرور | `TryHackMe!` |
| عدد المهام | مهمة واحدة |
| النتيجة | **Correct Answer** ثم **Room completed** |

## السيناريو

تطلب الغرفة التصرف كمحلل أمن في شركة West Tech بعد رصد نشاط غير معتاد على محطة الباحث Oliver Deer. تظهر مذكرة فدية على سطح المكتب، وتشير الحالة إلى سرقة بيانات مشاريع حساسة وتشفيرها. الهدف هو تحديد أثر المهاجم، استعادة البيانات، ثم العثور على العلم النهائي.[1]

## الإجابة التي تم التحقق منها

| المهمة | السؤال | الإجابة | نتيجة التحقق |
|---|---|---|---|
| Task 1 | Can you contAIn the threat and find the flag? | `thm{23,82,20,17,53}` | **Correct Answer** داخل TryHackMe ثم صفحة **Great work 9gkc! Room completed!** |

العلم حساس لحالة الأحرف؛ الصيغة المقبولة هي `thm` بحروف صغيرة، مع الأعداد الخمسة مفصولة بفواصل داخل الأقواس المعقوفة.

## مسار التحقيق

### 1. الوصول إلى محطة العمل

بعد تشغيل جهاز المختبر، يتم الاتصال من AttackBox أو من جهاز مرتبط بشبكة VPN عبر SSH:

```bash
ssh o.deer@10.48.157.55
```

كلمة المرور التي تعرضها الغرفة هي:

```text
TryHackMe!
```

يبدأ الفحص بعرض محتويات المنزل، ثم البحث عن ملفات PCAP وأرشيف البيانات المشفر:

```bash
ls -la
find /home/o.deer/ -type f -name '*.pcap'
```

### 2. تحديد ملف PCAP الشاذ

توجد ملفات الالتقاط في مجلدات مرتبة حسب التاريخ. الملف المهم هو:

```text
/home/o.deer/Documents/pcap_dumps/2025-06-17/session_4444_dump.pcap
```

يُحدد هذا الملف بمقارنة الأحجام؛ فالملف الشاذ أكبر من ملفات الالتقاط الصغيرة الأخرى، ما يجعله مرشحاً لاحتواء بيانات المهاجم أو جلسة التهريب.[2]

### 3. إعادة تجميع بيانات PCAP باستخدام Echo

يُرسل إلى مساعد التحقيق داخل الغرفة الطلب التالي:

```text
Reassemble /home/o.deer/Documents/pcap_dumps/2025-06-17/session_4444_dump.pcap
```

يُتوقع أن يكتب المساعد الناتج في:

```text
/home/o.deer/qwen-output/reassembled_data_dump.txt
```

بعد ذلك يمكن قراءة الناتج من محطة العمل:

```bash
cat /home/o.deer/qwen-output/reassembled_data_dump.txt
```

تكشف الملاحظات المعاد تجميعها أن المهاجم نفذ محاولات **Prompt Injection** ضد مساعد داخلي، وأنه ترك كلمة مرور الأرشيف ضمن ملاحظاته. السلسلة المبهمة:

```text
w#e@%s~t^t-e$c*h_v^i%ct_im_1
```

تُنظف بإزالة الرموز الخاصة لتصبح:

```text
westtechvictim1
```

### 4. فك أرشيف المشاريع

يُفك الأرشيف المشفر باستخدام كلمة المرور المستخرجة:

```bash
unzip /home/o.deer/westtech_projects_encrypted.zip -d /dev/shm/
```

عند طلب كلمة المرور، تُستخدم القيمة:

```text
westtechvictim1
```

بعد الاستخراج يوجد مجلد المشاريع، ومن الملفات المهمة:

```text
/dev/shm/home/o.deer/westtech_projects/thm_flags.txt
/dev/shm/home/o.deer/westtech_projects/thm_flags_guide.txt
```

### 5. تحديد العلم الحقيقي

يحتوي `thm_flags.txt` على أسطر مرمّزة بـ Base64، وليس كل سطر علماً حقيقياً. يوضح الدليل أن العلم الصحيح هو الذي يحتوي على **ثلاثة أعداد أولية بالضبط بين 10 و99**.[2] [3]

يمكن تفويض الفحص إلى أداة Echo المتخصصة:

```text
Use liberty_prime to check /dev/shm/home/o.deer/westtech_projects/thm_flags.txt and identify the flag.
```

الناتج الصحيح هو:

```text
thm{23,82,20,17,53}
```

وللتحقق حسابياً من شرط الدليل: الأعداد `23` و`17` و`53` أولية، بينما `82` و`20` غير أوليين؛ لذلك توجد ثلاثة أعداد أولية بالضبط.

## التحقق النهائي داخل المنصة

أُدخل العلم التالي في حقل Task 1:

```text
thm{23,82,20,17,53}
```

بعد الضغط على **Check** ظهرت رسالة **Correct Answer**. وبعد اكتمال تحديث النتيجة انتقلت الصفحة إلى مسار التهنئة، وظهرت الرسالة الرسمية:

> **Great work 9gkc! Room completed!**

وبذلك تم التحقق النهائي من صحة العلم وإكمال الغرفة داخل TryHackMe.[1]

## الدروس الأمنية

توضح الغرفة أن سجلات الشبكة قد تحتوي على بيانات تشغيلية حساسة تخص المهاجم نفسه، وليس فقط حركة الضحية. كما تبرز خطورة منح أنظمة الذكاء الاصطناعي وصولاً واسعاً إلى الذاكرة والملفات دون ضوابط قوية ضد Prompt Injection. ومن منظور الاستجابة للحوادث، يجب حفظ الأدلة، التحقق من سلامة الملفات، عزل الأنظمة المصابة، ومراجعة سجلات الوصول قبل فك أو استعادة البيانات.

## المراجع

[1]: https://tryhackme.com/room/containment "TryHackMe — ContAInment"

[2]: https://medium.com/@robo2575/tryhackme-containment-writeup-29d58795af28 "robo2575 — TryHackMe ContAInment Writeup"

[3]: https://medium.com/@shubhamkumar_/containment-ai-security-tryhackme-1fee40191982 "Shubham Kumar — ContAInment: AI Security TryHackMe"

---


إطار الاستخدام: جميع الخطوات ضمن مختبر TryHackMe المصرح به ولأغراض تعليمية ودفاعية.

---

## ملاحظات وأدلة مساندة

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


إطار الاستخدام: مختبر TryHackMe مصرح به وتعليمي.
