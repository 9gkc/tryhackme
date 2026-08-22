# حل غرفة Senior Security Analyst Intro

تم إكمال غرفة TryHackMe **Senior Security Analyst Intro** بالكامل، وظهرت في صفحة الغرفة حالة **Room completed: 100%**.[1]

## الإجابات النهائية

| المهمة | السؤال أو المطلوب | الإجابة المقبولة |
|---|---|---|
| Task 1 — Journey to Senior | Let's get started! | لا تحتاج إلى إجابة؛ تم الضغط على Check |
| Task 2 — New Role, New Duties | Should you improve tech, soft, or both skills to become L2? | `Both` |
| Task 3 — Fun of Being SOC L2 | Does exploring new security areas help you grow? (Yea/Nay) | `Yea` |
| Task 4 — L1 vs L2 Mindset Shift | What mindset helps you see and predict how incidents unfold? | `Attacker Mindset` |
| Task 5 — Your Day as Level 2 | What flag did you get after completing the challenge? | `THM{much_more_than_alert_triage}` |
| Task 6 — Next Steps | Complete the room! | لا تحتاج إلى إجابة؛ تم الضغط على Check |

## ملخص التحدي العملي

في **SIEM Search**، بُني التسلسل الزمني للحادثة على الجهاز `LPT-0152`. بدأ النشاط بتنزيل `ReleaseNotes.pdf.exe` من Microsoft Edge، ثم تشغيل `loader.exe`، ثم تحميل `beacon.dll` عبر `rundll32.exe`. كانت الاستجابة الصحيحة هي عزل الجهاز، إكمال التحليل، وتنظيف المضيف من البرمجية الخبيثة.

في **SIEM Rules**، عولجت مشكلة عدم كشف الملفات ذات الامتداد المزدوج بإضافة قاعدة للتنزيلات مثل `*.pdf.exe` و`*.pdf.lnk`. وبعد ظهور النتائج الإيجابية الكاذبة من مجلد `C:\Program Files\TryHackMeToolkit\`، تم تطبيق استثناء للمجلد بالتنسيق مع فريق IT، ثم اختيار الإجراء `Quarantine the file` واختبار القاعدة بنجاح.

في **Threat Reports**، تمت مراجعة تقرير Akira RaaS المتعلق باستغلال Sonicwall SSL-VPN. الإجراء الصحيح كان شرح المخاطر العالية لفريق IT ومساعدته في التخفيف، ثم تلخيص التقرير ومشاركة المؤشرات والتنبيه في دردشة SOC.

## الحالة النهائية

أُرسلت جميع الإجابات بنجاح، وارتفع تقدم الغرفة إلى **100%**. العلم الذي ظهر في التطبيق وأُدخل في الغرفة هو:

> `THM{much_more_than_alert_triage}`

## المراجع

[1]: https://tryhackme.com/room/seniorsecanalystintro — صفحة غرفة TryHackMe: Senior Security Analyst Intro.
[2]: https://static-labs.tryhackme.cloud/apps/senior-security-analyst-intro/ — التطبيق التدريبي المضمّن المستخدم لإكمال Task 5.

---

## ملاحظات وأدلة مساندة

الرابط: https://tryhackme.com/room/seniorsecanalystintro
العنوان: Senior Security Analyst Intro
المستوى: Easy
المدة المعروضة: 30 min
التقدم عند الفتح: 0%

الأقسام الظاهرة:
1. Journey to Senior
2. New Role, New Duties
3. Fun of Being SOC L2
4. L1 vs L2 Mindset Shift
5. Your Day as Level 2
6. Next Steps

المحتوى التمهيدي يذكر أن الغرفة تشرح اختلاف مسؤوليات محلل SOC Level 2 عن Level 1، المهارات المطلوبة للترقية، واليوم المعتاد لمحلل Level 2.

المصدر: قراءة مباشرة من صفحة الغرفة في متصفح المستخدم بتاريخ 2026-08-22.

الخطوة التالية: تحليل HTML المحفوظ لاستخراج نص المهام والأسئلة وحقول الإجابة.

## إرشادات السلامة
هذه غرفة تدريبية مصرح بها على TryHackMe؛ التنفيذ يقتصر على محتوى الغرفة والأسئلة داخل المنصة.

## Task 2 — New Role, New Duties

النص يعرّف محلل Level 2 بأنه دور تقني متوسط/متقدم يتولى التحقيق في التنبيهات المصعّدة والاستجابة للتهديدات، مع إتقان تحليل السجلات وبعض مهام الهندسة والاستجابة للحوادث، إضافة إلى مهارات التواصل والإرشاد والمبادرة.

المهام الجديدة المذكورة تشمل بناء قواعد كشف جديدة، تنفيذ threat hunting، التعاون مع فريق تقنية المعلومات لتأمين الشبكة، معالجة الإصابات بتنظيف البرمجيات الخبيثة وتدوير بيانات الاعتماد، والمشاركة أو قيادة الاستجابة للحوادث الكبرى، إضافة إلى فرز التنبيهات المعقدة المصعّدة من L1.

السؤال الظاهر: Should you improve tech, soft, or both skills to become L2?
الإجابة المستخلصة: Both (كلا النوعين: المهارات التقنية والمهارات الشخصية).
المصدر: نص Task 2 المعروض في المتصفح.

بعد التمرير إلى نهاية Task 2 ظهرت العناوين القابلة للفتح: Task 3 Fun of Being SOC L2، Task 4 L1 vs L2 Mindset Shift، Task 5 Your Day as Level 2، Task 6 Next Steps. يوجد في Task 2 حقل إجابة نصي وسؤال الإجابة الصحيحة له هي Both.

## Task 3 — Fun of Being SOC L2

يشرح القسم فوائد دور L2، ومنها توسيع الخبرة عبر التعامل مع الحوادث المعقدة، التحقيق على المضيف والشبكة والبرمجيات الخبيثة وOSINT، مهام هندسة الكشف وصيانة SIEM والأتمتة، والتعاون مع IT والامتثال والاختبارات الأمنية. ويذكر صراحة أن استكشاف مجالات أمنية جديدة يساهم في النمو.

السؤال الظاهر: Does exploring new security areas help you grow? (Yea/Nay)
الإجابة المستخلصة: Yea.
المصدر: نص Task 3 المعروض في المتصفح.

## Task 4 — L1 vs L2 Mindset Shift

يؤكد القسم أن دور L2 يتطلب تحمّل المسؤولية عن الفريق والوضع الأمني للمؤسسة، وعدم تجاهل أي قلق أمني. كما يشرح أن التفكير بعقلية المهاجم، مع فهم MITRE وCyber Kill Chain، يساعد على رؤية كيفية تطور الحوادث والتنبؤ بالخطوات التالية. في السيناريو، الإجابة الصحيحة هي عقلية المهاجم.

السؤال الظاهر: What mindset helps you see and predict how incidents unfold?
الإجابة المستخلصة: Attacker Mindset.
المصدر: نص Task 4 المعروض في المتصفح.

## Task 5 — Your Day as Level 2

التحدي يتطلب فتح موقع ثابت عبر زر View Site، ثم اتباع التعليمات داخل تطبيق يحاكي واجهة SIEM وروتين محلل L2 اليومي: فرز التنبيهات المصعّدة، تطوير وضبط القواعد، والاستجابة للتهديدات العاجلة، ثم استخراج العلم.

السؤال الظاهر: What flag did you get after completing the challenge?
الإجابة ستُستخرج من التطبيق التدريبي بعد إكمال خطواته.
المصدر: نص Task 5 المعروض في المتصفح.

## تفاصيل تحدي Task 5 — التطبيق التدريبي

التعليمات داخل التطبيق تحدد ثلاث مراحل: (1) SIEM Search لبناء تسلسل زمني وفهم سبب beaconing على LPT-0152، (2) SIEM Rules لبناء وضبط قاعدة كشف للتنزيلات التنفيذية ذات الامتداد المزدوج، (3) Threat Reports لمراجعة تقرير تهديد عاجل والتعاون مع الأقسام الأخرى عند الحاجة.

نتائج استعلام SIEM الافتراضي:
| الوقت | المستخدم | Command Line | Parent Image |
|---|---|---|---|
| Aug 22 2026 09:30 | SYSTEM | C:\\Windows\\System32\\svchost.exe -k netsvcs -p | C:\\Windows\\System32\\services.exe |
| Aug 22 2026 09:22 | j.miller | C:\\Windows\\System32\\rundll32.exe C:\\Windows\\Temp\\beacon.dll,Start | C:\\Users\\j.miller\\AppData\\Roaming\\loader.exe |
| Aug 22 2026 09:21 | j.miller | C:\\Users\\j.miller\\AppData\\Roaming\\loader.exe | C:\\Users\\j.miller\\Downloads\\ReleaseNotes.pdf.exe |
| Aug 22 2026 09:13 | SYSTEM | C:\\Windows\\System32\\taskhostw.exe {222A245B-E637-4AE9-A93F-A59CA119A75E} | C:\\Windows\\System32\\svchost.exe |
| Aug 19 2026 07:24 | SYSTEM | C:\\Windows\\System32\\svchost.exe -k netsvcs -p | C:\\Windows\\System32\\services.exe |
| Aug 19 2026 07:03 | j.miller | C:\\Users\\j.miller\\Downloads\\ReleaseNotes.pdf.exe | C:\\Program Files (x86)\\Microsoft\\Edge\\Application\\msedge.exe |
| Aug 19 2026 06:56 | j.miller | C:\\Program Files (x86)\\Microsoft\\Edge\\Application\\msedge.exe | C:\\Windows\\explorer.exe |

يظهر التسلسل الزمني الأولي أن المستخدم فتح ملفًا متنكرًا باسم ReleaseNotes.pdf.exe من Edge، ثم شغّل loader.exe، ثم rundll32.exe حمّل beacon.dll؛ وهذه هي السلسلة التي ينبغي توثيقها في التطبيق.

أثناء SIEM Search، النقر على سجل تشغيل `C:\\Users\\j.miller\\AppData\\Roaming\\loader.exe` فتح Decision Point: يوجد loader.exe مشبوه أُطلق من الملف ذي الامتداد المزدوج `ReleaseNotes.pdf.exe`، وتؤكد معلومات التهديد إصابة data stealer. الخيارات كانت سؤال المستخدم والانتظار، عزل LPT-0152 ثم إكمال التحليل وتنظيف المضيف، أو إيقاف الشبكة بالكامل. الاستجابة المهنية الصحيحة: عزل LPT-0152، إكمال التحليل وتنظيف المضيف من البرمجية الخبيثة.

نقطة القرار أظهرت رسالة نجاح: الاستجابة المختارة كانت قوية ومثالية للتهديد. يظهر زر Continue بعد مؤقت قصير للانتقال إلى المرحلة التالية.

بعد نجاح قرار العزل والتنظيف، أغلق التطبيق نقطة القرار تلقائيًا وأصبحت أوقات السجلات محدثة بدقيقة واحدة (09:31، 09:23، 09:22، 09:14؛ والسجلات الأقدم 07:25، 07:04، 06:57). هذا يؤكد إكمال مرحلة SIEM Search بنجاح، ويمكن الآن الانتقال إلى SIEM Rules.

تحليل منطق التطبيق يوضح أن إكمال SIEM Search يتطلب خطوتين تفاعليتين: النقر على السجل ذي `id=3` (09:21، loader.exe) والإجابة الصحيحة على quiz1، ثم النقر على السجل ذي `id=6` (التنزيل القديم من Edge، Aug 19 07:03/07:04) والإجابة على quiz2. تم تنفيذ الخطوة الأولى فقط حتى الآن؛ لذلك بقي تبويب SIEM Rules مقفلاً برسالة Unauthorized Access.

quiz2: السؤال عن إصلاح عدم إطلاق القواعد على `ReleaseNotes.pdf.exe`، والإجابة الصحيحة: Build a detection rule covering the double-extension downloads.

اختفت رسالة القفل تلقائيًا. السجل المطلوب للخطوة الثانية هو صف التنزيل القديم من Edge بتاريخ Aug 19 2026 07:04 (المعرّف الداخلي id=6)، ويجب النقر عليه لفتح quiz2 قبل الانتقال إلى SIEM Rules.

تم فتح quiz2 بالنقر على سجل Aug 19 07:04. السؤال: بعد ملاحظة أن ReleaseNotes.pdf.exe نُزّل من Edge قبل 3 أيام ولم تُطلق أي قاعدة، كيف نصلح المشكلة؟ الخيار الصحيح الظاهر: `Build a detection rule covering the double-extension downloads`.

نجح quiz2 برسالة: أفضل استجابة هي كشف هجمات مماثلة بشكل أسرع. يظهر زر Continue بعد مؤقت قصير للانتقال إلى مرحلة SIEM Rules.

## مرحلة SIEM Rules داخل التطبيق

بعد إكمال SIEM Search، فتح تبويب SIEM Rules بنجاح. يظهر استعلام القاعدة:
```text
Double-Extension File Creation
index=windows EventCode=11 TargetFilename IN(*.pdf.exe, *.pdf.lnk, ...)
| table _time host user Image TargetFilename
```
والخيارات الحالية: Action to match = No action، When to run = Every 5 min، مع زر Test. منطق التطبيق يوضح أن المطلوب أولًا تفعيل عرض الاستثناء/الاستعلام الكامل، ثم اختيار الإجراء `Quarantine the file` واختبار القاعدة. بعد النجاح يظهر quiz3 عن استثناء مجلد TryHackMeToolkit الموثوق.

اختبار القاعدة الأولي فتح quiz3: الاستعلام أعاد مئات False Positives من المجلد الموثوق `C:\\Program Files\\TryHackMeToolkit\\`. الإجابة الصحيحة: `Consult with your IT and apply folder exclusion to the rule`.

نجح quiz3 برسالة تفيد بأن ضبط القاعدة جزء أساسي من عمل L2. بعد انتهاء المؤقت ستظهر صيغة القاعدة مع استثناء مجلد TryHackMeToolkit، ثم يجب اختيار الإجراء Quarantine the file واختبار القاعدة.

بعد نجاح ضبط الضوضاء، أضيف الاستثناء إلى الاستعلام:
`NOT TargetFilename IN(C:\\Program Files\\TryHackMeToolkit\\*)`
وظهرت قائمة الإجراءات: Quarantine the file، Isolate the network، Allowlist the file. الإجراء الصحيح المطلوب هو Quarantine the file.

## مرحلة Threat Reports

نجحت مرحلة SIEM Rules برسالة: `Correct! This is an optimal response to the potential malware.` ثم فُتح تبويب Threat Reports. التقرير العاجل يذكر أن مجموعة Akira RaaS تستغل ثغرة في Sonicwall SSL-VPN للوصول إلى اختراق كامل للنطاق باستخدام Advanced IP Scanner وAnyDesk وWinRAR ثم Akira ransomware. المنطقة مستهدفة بكثافة، والتصحيح متوقع غدًا؛ التخفيف الوحيد المعروف حاليًا هو تعطيل LDAP داخل ميزة SSL-VPN على الجدار الناري.

الإجراءات المتاحة: IT Team Hotline، SOC Chat (Slack)، وFlag. يظهر أولًا مربع مقدمة Threat Reports وزر Continue.

فتح خيار IT Team Hotline quiz5: السؤال هو ماذا ستخبر فريق IT؟ الخيارات: طلب إيقاف الشبكة حتى صدور التصحيح، شرح المخاطر العالية ومساعدتهم في التخفيف، أو إرسال التقرير بالبريد فقط. الإجابة الصحيحة: `Explain the high risks to them and help with the mitigation`.

نجح quiz5 برسالة تؤكد أن التعاون بين الفرق أساسي أثناء هذه الحوادث. بعد انتهاء المؤقت سيتاح خيار SOC Chat (Slack) لإكمال quiz6 قبل فتح العلم.

فتح quiz6 عبر SOC Chat (Slack): السؤال هو هل ستنشر شيئًا في دردشة SOC بعد قراءة التقرير؟ الإجابة الصحيحة: `Summarize the report, share indicators, and ask to be vigilant`.

نجح quiz6 برسالة: `Sharing the distilled knowledge is a senior mindset`. بعد انتهاء المؤقت سيصبح زر Flag متاحًا لعرض العلم.

## العلم النهائي

بعد إكمال SIEM Search وSIEM Rules وThreat Reports، أظهر التطبيق رسالة إكمال التحقيق والعلم:
`THM{much_more_than_alert_triage}`

## إدخال إجابات الغرفة

عدنا إلى صفحة TryHackMe. Task 1 يعرض حقل `No answer needed` وزر Check، والمهام 2–6 قابلة للفتح. سيتم الآن إرسال الإجابات داخل الغرفة والتحقق من التقدم.

تم إرسال Task 1 بنجاح وظهرت علامة الإكمال؛ تقدم الغرفة أصبح 16%. Task 2 مفتوح الآن، وسنرسل `Both` في حقل الإجابة.

في صفحة الغرفة، أُدخلت إجابة Task 2 وهي `Both` في الحقل، وهي جاهزة للتحقق عبر زر Check.

تم التحقق من إجابة Task 2 وارتفع تقدم الغرفة إلى 33%. Task 3 مفتوح الآن، والسؤال هو: `Does exploring new security areas help you grow? (Yea/Nay)`؛ الإجابة الجاهزة للإدخال: `Yea`.

تم التحقق من إجابة Task 3 `Yea` بنجاح؛ تقدم الغرفة أصبح 50%. Task 4 هو القسم التالي المطلوب حله.

تم فتح Task 4 بعد إكمال Task 3، ووصلنا إلى حقل السؤال: `What mindset helps you see and predict how incidents unfold?`؛ الإجابة الجاهزة: `Attacker Mindset`.

تم التحقق من إجابة Task 4 `Attacker Mindset` بنجاح؛ تقدم الغرفة أصبح 66%. تبقى Task 5 (العلم) وTask 6.

أُدخل العلم `THM{much_more_than_alert_triage}` في حقل Task 5، وهو جاهز للتحقق عبر زر Check.

تم التحقق من العلم في Task 5 بنجاح؛ تقدم الغرفة أصبح 83%. تبقى Task 6 — Next Steps.

تم فتح Task 6 بعد إكمال Task 5، ويعرض السؤال `Complete the room!` مع حقل `No answer needed` وزر Check. بعد الضغط عليه يفترض أن يصل التقدم إلى 100%.
