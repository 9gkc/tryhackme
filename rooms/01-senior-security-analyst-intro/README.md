# Senior Security Analyst Intro — TryHackMe

> **الحالة:** تم إكمال الغرفة بالكامل؛ تظهر في صفحة الغرفة عبارة Room completed: 100%، وجميع الإجابات مقبولة بما فيها العلم النهائي [1]. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| العنصر | القيمة |
|---|---|
| الرابط | [Senior Security Analyst Intro][1] |
| التصنيف/المجال | — |
| الصعوبة | Easy |
| المدة | 30 min |
| المختبر | [التطبيق التدريبي المضمّن لتحدي Task 5][2] |

## الملخص التنفيذي

تقدم الغرفة تصوراً عملياً لدور SOC L2 عبر ست مهام مترابطة تغطي التحول الذهني بين L1 وL2، المهارات المطلوبة، واليوم الاعتيادي لمحلل L2 الذي يجمع بين فرز التنبيهات المصعّدة، هندسة الكشف، والاستجابة للحوادث، مع التعاون بين الفرق واستيعاب تقارير التهديدات الحديثة.

تضمّن الجانب العملي بناء تسلسل زمني لحادثة على المضيف LPT-0152، ضبط قاعدة SIEM لاكتشاف تنزيلات الملفات ذات الامتداد المزدوج، استبعاد مصدر موثوق للحد من الإيجابيات الكاذبة، اختيار إجراء الحجر للملفات الخبيثة، ومراجعة تقرير تهديد عاجل حول Akira RaaS واستغلال Sonicwall SSL-VPN والتنسيق مع فريق IT. انتهت التجربة باستخراج العلم THM{much_more_than_alert_triage} من التطبيق التدريبي ثم إدخاله في الغرفة.

## مسار الحل

### 1. SIEM Search — بناء التسلسل الزمني واتخاذ قرار الاستجابة

تم تحليل السجلات لبناء تسلسل زمني لنشاط المضيف LPT-0152 الذي يفسّر الـ beaconing. السجلات المفصلّة أوضحت سلسلة تنفيذ خبيثة بدأت بتنزيل ملف بامتداد مزدوج، ثم مُحمّل، ثم تحميل DLL عبر rundll32:

| الوقت | المستخدم | Command Line | Parent Image |
|---|---|---|---|
| Aug 22 2026 09:30 | SYSTEM | C:\Windows\System32\svchost.exe -k netsvcs -p | C:\Windows\System32\services.exe |
| Aug 22 2026 09:22 | j.miller | C:\Windows\System32\rundll32.exe C:\Windows\Temp\beacon.dll,Start | C:\Users\j.miller\AppData\Roaming\loader.exe |
| Aug 22 2026 09:21 | j.miller | C:\Users\j.miller\AppData\Roaming\loader.exe | C:\Users\j.miller\Downloads\ReleaseNotes.pdf.exe |
| Aug 22 2026 09:13 | SYSTEM | C:\Windows\System32\taskhostw.exe {222A245B-E637-4AE9-A93F-A59CA119A75E} | C:\Windows\System32\svchost.exe |
| Aug 19 2026 07:24 | SYSTEM | C:\Windows\System32\svchost.exe -k netsvcs -p | C:\Windows\System32\services.exe |
| Aug 19 2026 07:03 | j.miller | C:\Users\j.miller\Downloads\ReleaseNotes.pdf.exe | C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe |
| Aug 19 2026 06:56 | j.miller | C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe | C:\Windows\explorer.exe |

- نقطة القرار الأولى (على سجل loader.exe): وُصف loader.exe كمشبوه انطلق من ReleaseNotes.pdf.exe ذي الامتداد المزدوج، مع تأكيد إصابة data stealer. الخيار الصحيح: عزل الجهاز LPT-0152، إكمال التحليل، وتنظيف المضيف من البرمجية الخبيثة. ظهرت رسالة نجاح تفيد بأن الاستجابة قوية ومثالية، ثم استُكمل التحدي.
- نقطة القرار الثانية (على سجل تنزيل Edge الأقدم): أصل المشكلة أن قواعد SIEM لم تكشف تنزيل ReleaseNotes.pdf.exe. الحل الصحيح: بناء قاعدة كشف تستهدف تنزيلات الامتداد المزدوج. بعد القبول فُتح تبويب SIEM Rules.

ملاحظات تنفيذية داخل التطبيق:
- إتمام هذه المرحلة تطلب التفاعل مع سجل Aug 22 09:21 (loader.exe، id=3) ثم سجل Aug 19 07:03/07:04 (تنزيل Edge، id=6). بعد النجاح تحدّثت الطوابع الزمنية دقيقة للأعلى (09:31، 09:23، 09:22، 09:14 …) كتغذية راجعة مرئية على التقدم.

### 2. SIEM Rules — بناء القاعدة، تقليل الضوضاء، والإجراء المناسب

عُرض استعلام مبدئي لقاعدة "Double-Extension File Creation" على نافذة SIEM:

```
Double-Extension File Creation
index=windows EventCode=11 TargetFilename IN(*.pdf.exe, *.pdf.lnk, ...)
| table _time host user Image TargetFilename
```

- الاختبار الأولي أعاد مئات الإيجابيات الكاذبة من مجلد موثوق: C:\Program Files\TryHackMeToolkit\.
- القرار الصحيح لتقليل الضوضاء: التنسيق مع فريق IT وتطبيق استثناء للمجلد ضمن القاعدة. بعد القبول عُدّل الاستعلام بإضافة الاستثناء:

```
NOT TargetFilename IN(C:\Program Files\TryHackMeToolkit\*)
```

- بعد ضبط الضوضاء، عُرضت إجراءات الاستجابة: Quarantine the file، Isolate the network، Allowlist the file. الإجراء الصحيح: Quarantine the file.
- ظهرت رسالة نجاح: "Correct! This is an optimal response to the potential malware." ثم فُتح تبويب Threat Reports.

### 3. Threat Reports — الاستيعاب والتنسيق بين الفرق

عُرض تقرير عاجل حول Akira RaaS يستغل ثغرة في Sonicwall SSL-VPN وصولاً لاختراق كامل للنطاق باستخدام Advanced IP Scanner وAnyDesk وWinRAR ثم Akira ransomware. المنطقة مستهدفة بكثافة، والتصحيح متوقع غداً؛ التخفيف الوحيد المعروف حالياً هو تعطيل LDAP ضمن ميزة SSL-VPN على الجدار الناري.

- IT Team Hotline: الإجابة الصحيحة كانت Explain the high risks to them and help with the mitigation. ظهرت رسالة تؤكد أهمية التعاون بين الفرق.
- SOC Chat (Slack): الإجابة الصحيحة كانت Summarize the report, share indicators, and ask to be vigilant، مع تغذية راجعة: "Sharing the distilled knowledge is a senior mindset".
- Flag: بعد قبول الخطوتين أصبح زر العلم متاحاً، وعُرض العلم النهائي من التطبيق:

THM{much_more_than_alert_triage}

## الإجابات النهائية

| المهمة | السؤال أو المطلوب | الإجابة المقبولة |
|---|---|---|
| Task 1 — Journey to Senior | Let's get started! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| Task 2 — New Role, New Duties | Should you improve tech, soft, or both skills to become L2? | `Both` |
| Task 3 — Fun of Being SOC L2 | Does exploring new security areas help you grow? (Yea/Nay) | `Yea` |
| Task 4 — L1 vs L2 Mindset Shift | What mindset helps you see and predict how incidents unfold? | `Attacker Mindset` |
| Task 5 — Your Day as Level 2 | What flag did you get after completing the challenge? | `THM{much_more_than_alert_triage}` |
| Task 6 — Next Steps | Complete the room! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |

## التحقق الرسمي داخل TryHackMe

- على صفحة الغرفة يظهر المؤشر Room completed: 100% كدليل مرئي على الإكمال [1].
- أثناء إدخال الإجابات، أظهر كل زر Check قبول الإجابة وتقدّم الشريط تدريجياً حتى 100%. العلم THM{much_more_than_alert_triage} قُبل في Task 5.
- داخل التطبيق التدريبي [2] ظهرت رسائل نجاح صريحة عند كل قرار صحيح، مثل:
  - "Correct! This is an optimal response to the potential malware." في مرحلة SIEM Rules.
  - رسائل نجاح وتفعيل أزرار Continue بعد مؤقتات قصيرة في كل Quiz.
  - فتح التبويبات المقفلة بعد تحقيق المتطلبات (زوال "Unauthorized Access" عند الانتقال من SIEM Search إلى SIEM Rules).
- لم يُرسل تقييم الغرفة؛ جميع الإجابات أُدخلت وقُبلت، واكتمل تقدم الغرفة إلى 100%.

## الدروس الأمنية

- تبنّي Attacker Mindset مع فهم مراحل الهجوم يساعد على توقع الخطوات التالية وبناء تسلسل زمني دقيق للحوادث.
- هندسة الكشف لا تنجح دون ضبط الضوضاء والتنسيق مع فرق IT لإدارة الاستثناءات الموثوقة، مع اختيار إجراء استجابة مناسب مثل Quarantine.
- متابعة تقارير التهديدات العاجلة وترجمتها إلى إجراءات تخفيف عملية وتواصل فعّال داخل الفريق يعكسان دور L2 الناضج الذي يتجاوز فرز التنبيهات إلى قيادة الاستجابة.

## المراجع

[1]: https://tryhackme.com/room/seniorsecanalystintro
[2]: https://static-labs.tryhackme.cloud/apps/senior-security-analyst-intro/
