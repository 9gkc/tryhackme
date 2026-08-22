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
