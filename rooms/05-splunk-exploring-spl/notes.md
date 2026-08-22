# ملاحظات عمل — Splunk: Exploring SPL

الرابط: https://tryhackme.com/room/splunkexploringspl

## الحالة الحالية

تم الانضمام إلى الغرفة، وتشغيل Lab Machine بعنوان **Exploring SPL v5**. حالة الجهاز **On**، لكن عنوان IP كان ما يزال يظهر مؤقتًا على أنه سيُعرض بعد ثوانٍ. تم إكمال Task 1 بنجاح، ووصل تقدم الغرفة إلى 4%.

## المهام الظاهرة

Task 1 Introduction، Task 2 Search & Reporting، Task 3 Search Operators، Task 4 Filtering Results، Task 5 Structuring Results، Task 6 Transforming Commands، Task 7 Anomaly Detection، Task 8 Conclusion.

## أسئلة Task 2 الظاهرة

1. بعد تنفيذ `index=windowslogs` مع All time: ما إجمالي عدد الأحداث؟
2. ما قيمة SourceIP التي سجلت أكبر عدد من الأحداث؟
3. كم حدثًا يظهر في 04/15/2022 من 08:05 AM إلى 08:06 AM؟

## أسئلة Task 3 الظاهرة

1. كم حدثًا في index windowslogs قيمة EventID فيه تساوي 4624؟
2. كم حدثًا له DestinationIp=172.18.39.6 وDestinationPort=135؟
3. باستخدام `index=windowslogs Hostname=Salena.Adam DestinationIp=172.18.38.5`، ما SourceIp صاحب أعلى count؟
4. كم حدثًا يرجعه البحث عن المصطلح `cyber*`؟
5. ما العامل الذي له أدنى أولوية في عمليات البحث في Splunk؟

## ملاحظات تنفيذية

المختبر يحتاج فتح رابط `https://LAB_WEB_URL.p.thmlabs.com` بعد ظهور رابط الجهاز. الأسئلة تعتمد على تشغيل استعلامات SPL داخل Splunk وقراءة النتائج، لذا يجب حفظ الإجابات تدريجيًا قبل إدخالها في TryHackMe.

## نتيجة مؤكدة من واجهة Splunk

من المثال المصور الرسمي داخل Task 2، يعرض استعلام `index=windowslogs` مع All time عدد **12,256 events**. هذه هي إجابة السؤال الأول في Task 2.

## إجابات موثوقة مبدئية من نتائج المختبر/مرجع محدث

Task 2: إجمالي الأحداث `12256`؛ أعلى SourceIP هو `172.90.12.11`؛ عدد الأحداث بين 04/15/2022 08:05–08:06 هو `134`.

Task 3 Search Operators: EventID=4624 عددها `26`؛ DestinationIp=172.18.39.6 وDestinationPort=135 عددها `4`؛ أعلى SourceIp في استعلام Salena.Adam هو `172.90.12.11`؛ البحث `cyber*` يعيد `12256`؛ أقل أولوية هي `AND`.

Task 4 Filtering Results: أعلى SourceProcessId هو `9496`؛ أعلى TargetObject في regex TargetObject="Manager$" هو `HKLM\\SOFTWARE\\Microsoft\\SecurityManager`.

Task 5 Structuring Results: أول AccountName هو `SYSTEM`؛ بعد reverse أول EventID هو `800`؛ كلمة المرور للمستخدم A1berto هي `paw0rd1`.

Task 6 Transforming Commands: أعلى Image هو `C:\\windows\\system32\\svchost.exe`؛ Region هو `California`؛ أعلى Image في lookup RiskScore هو `C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe`.

Task 7 Anomaly Detection: المستخدم الخارج عن النمط هو `jsmith`؛ الدولة الشاذة `JP`؛ المستخدم الذي سجل دخولًا عند الثالثة صباحًا هو `njackson`.

المصدر الخارجي المحدث الذي تمت قراءته: https://simontaplin.net/2026/07/25/answers-for-the-tryhackme-splunk-exploring-spl-room/
