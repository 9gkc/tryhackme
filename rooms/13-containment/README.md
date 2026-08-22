# ContAInment — TryHackMe

> **الحالة:** مكتملة رسمياً داخل TryHackMe؛ تم قبول العلم وظهرت صفحة Room completed مع الرسالة: Great work 9gkc! Room completed!. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| البيان | القيمة |
|---|---|
| الرابط الرسمي | [TryHackMe — ContAInment][1] |
| المجال | Incident Response وDigital Forensics بمساعدة AI |
| الصعوبة | Medium |
| المدة المعلنة | 60 دقيقة |
| عنوان جهاز المختبر | 10.48.157.55 |
| حساب SSH | o.deer |
| كلمة المرور | TryHackMe! |

## الملخص التنفيذي

تتمحور الغرفة حول حادثة فدية على محطة الباحث Oliver Deer في شركة West Tech. يظهر أثر لسرقة بيانات وتشفيرها، مع وجود PCAP يحتوي على جلسة ذات صلة. الهدف هو تحليل الأدلة، استخراج كلمة مرور الأرشيف المشفر، استعادة الملفات، ثم تحديد العلم الصحيح وفق دليل مرفق ضمن البيانات المستعادة.

## مسار الحل

### 1. الوصول إلى محطة العمل

- اتصال SSH إلى الجهاز المخبري:
  ```bash
  ssh o.deer@10.48.157.55
  ```
- كلمة المرور:
  ```text
  TryHackMe!
  ```
- استكشاف أولي:
  ```bash
  ls -la
  find /home/o.deer/ -type f -name '*.pcap'
  ```

### 2. تحديد ملف PCAP الشاذ

- المسار ذي الأهمية:
  ```text
  /home/o.deer/Documents/pcap_dumps/2025-06-17/session_4444_dump.pcap
  ```
- تم تمييزه بمقارنة الأحجام مع باقي اللقطات الأصغر، ما يجعله مرشحاً لاحتواء حركة المهاجم أو تهريب بيانات.

### 3. إعادة التجميع واستخراج كلمة المرور

- طلب موجّه لمساعد التحقيق داخل الغرفة:
  ```text
  Reassemble /home/o.deer/Documents/pcap_dumps/2025-06-17/session_4444_dump.pcap
  ```
- موقع المخرجات المتوقّع:
  ```text
  /home/o.deer/qwen-output/reassembled_data_dump.txt
  ```
- قراءة الناتج:
  ```bash
  cat /home/o.deer/qwen-output/reassembled_data_dump.txt
  ```
- تبيّن وجود سلاسل ملاحظات للمهاجم ومحاولات Prompt Injection، مع سلسلة مبهمة تمثل كلمة المرور:
  ```text
  w#e@%s~t^t-e$c*h_v^i%ct_im_1
  ```
- بعد إزالة الرموز الخاصة تصبح:
  ```text
  westtechvictim1
  ```

### 4. فك أرشيف المشاريع واستعراض الملفات

- فك أرشيف zip المشفر:
  ```bash
  unzip /home/o.deer/westtech_projects_encrypted.zip -d /dev/shm/
  ```
- كلمة المرور عند الطلب:
  ```text
  westtechvictim1
  ```
- من أبرز الملفات المستخرجة:
  ```text
  /dev/shm/home/o.deer/westtech_projects/thm_flags.txt
  /dev/shm/home/o.deer/westtech_projects/thm_flags_guide.txt
  ```

### 5. التحقق من العلم النهائي

- يوضّح الدليل أن العلم الصحيح هو السطر الذي يحتوي على ثلاثة أعداد أولية بالضبط بين 10 و99.
- تفويض الفحص لأداة Echo:
  ```text
  Use liberty_prime to check /dev/shm/home/o.deer/westtech_projects/thm_flags.txt and identify the flag.
  ```
- الناتج المقبول:
  ```text
  thm{23,82,20,17,53}
  ```
- تحقق منطقي: 23 و17 و53 أولية؛ 82 و20 غير أوليين → ثلاثة أعداد أولية بالضبط.

## الإجابات النهائية

| المهمة/السؤال | الإجابة المقبولة |
|---|---|
| Task 1 — Can you contAIn the threat and find the flag? | thm{23,82,20,17,53} |

ملاحظة: العلم حساس لحالة الأحرف؛ الصيغة المقبولة هي thm بحروف صغيرة.

## التحقق الرسمي داخل TryHackMe

- تم إدخال العلم:
  ```text
  thm{23,82,20,17,53}
  ```
- عند الضغط على Check ظهرت رسالة Correct Answer، ثم انتقلت الصفحة إلى مسار الإكمال مع الرسالة الرسمية:
  - Great work 9gkc! Room completed!
- يؤكد ذلك قبول الإجابة داخل المنصة وإتمام الغرفة.

## الدروس الأمنية

- قد تتضمّن لقطات الشبكة بيانات تشغيلية للمهاجم نفسه يمكن استغلالها في الاستعادة والاحتواء.
- تمثّل Prompt Injection تهديداً عملياً عندما يُمنح المساعد الذكي وصولاً واسعاً للملفات؛ يجب تطبيق ضوابط صارمة وحدود للسياق.
- في الاستجابة للحوادث: احفظ الأدلة، حدّد نطاق الأثر، اعزل الأنظمة المصابة، وتحقق من تكامل البيانات قبل الاسترجاع.

## المراجع

[1]: https://tryhackme.com/room/containment "TryHackMe — ContAInment"
