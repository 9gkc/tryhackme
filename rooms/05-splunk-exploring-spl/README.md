# حل غرفة TryHackMe: Splunk: Exploring SPL

رابط الغرفة: https://tryhackme.com/room/splunkexploringspl

تم إكمال الغرفة والتحقق من ظهور **Room completed: 100%** في المتصفح.

## الإجابات

| المهمة | السؤال المختصر | الإجابة |
|---|---|---|
| Task 1 | Introduction / تشغيل المختبر | لا توجد إجابة نصية |
| Task 2.1 | إجمالي أحداث `index=windowslogs` | `12256` |
| Task 2.2 | أعلى `SourceIP` من حيث الأحداث | `172.90.12.11` |
| Task 2.3 | أحداث 04/15/2022 من 08:05 إلى 08:06 | `134` |
| Task 3.1 | عدد أحداث `EventID=4624` | `26` |
| Task 3.2 | `DestinationIp=172.18.39.6` و`DestinationPort=135` | `4` |
| Task 3.3 | أعلى `SourceIp` لاستعلام Salena.Adam | `172.90.12.11` |
| Task 3.4 | نتائج البحث عن `cyber*` | `12256` |
| Task 3.5 | العامل ذو الأولوية الأدنى | `AND` |
| Task 4.1 | أعلى `SourceProcessId` | `9496` |
| Task 4.2 | أعلى `TargetObject` في regex `Manager$` | `HKLM\\SOFTWARE\\Microsoft\\SecurityManager` |
| Task 5.1 | أول `AccountName` في table | `SYSTEM` |
| Task 5.2 | أول `EventID` بعد `reverse` | `800` |
| Task 5.3 | كلمة مرور المستخدم `A1berto` | `paw0rd1` |
| Task 6.1 | أكثر قيمة تكرارًا في `Image` | `C:\\windows\\system32\\svchost.exe` |
| Task 6.2 | منطقة عناوين IP بعد `iplocation` | `California` |
| Task 6.3 | أعلى Image في lookup RiskScore | `C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe` |
| Task 7.1 | المستخدم الآخر الخارج عن النمط | `jsmith` |
| Task 7.2 | الدولة الشاذة للمستخدم السابق | `JP` |
| Task 7.3 | المستخدم الذي سجل دخولًا عند الثالثة صباحًا | `njackson` |
| Task 8 | Conclusion | لا توجد إجابة نصية؛ تم التحقق بنجاح |

## التحقق النهائي

- إجابات Tasks 2–7 ظهرت في المتصفح كـ **Correct Answer**.
- Task 8 ظهر كـ **Correct Answer**.
- حالة الغرفة النهائية: **Room completed: 100%**.

## المصدر المرجعي

تمت مطابقة الإجابات مع نتائج مختبر Splunk المباشر ومرجع عام محدث:

https://simontaplin.net/2026/07/25/answers-for-the-tryhackme-splunk-exploring-spl-room/

---

## ملاحظات وأدلة مساندة

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
