# Threat Hunting: Introduction — notes

رابط الغرفة: https://tryhackme.com/room/threathuntingintroduction

## الإجابات المرجعية المستخرجة

| القسم | السؤال | الإجابة |
|---|---|---|
| Task 1 | What is the average number of days an attacker remains undetected in a network called? | `Dwell time` |
| Task 1 | Is threat hunting reactive or proactive? | `Proactive` |
| Task 2 | Which threat hunting approach would you use if you have received threat intelligence about an APT group targeting your industry? | `Intelligence-Driven Hunting` |
| Task 2 | Which threat hunting approach is most efficient when you have a list of file hashes and IOCs from a threat feed? | `Intelligence-Driven Hunting` |
| Task 3 | What category of hunting target represents artifacts left behind by attackers during their attack? | `Attack Residues` |
| Task 4 | Which hunting technique uses file hashes, IP addresses, and domain names to search for specific artifacts? | `Indicators of Compromise` |
| Task 4 | What hunting technique is represented by searching for “Word.exe spawns cmd.exe spawns powershell.exe that connects to external IP”? | `Behavioral Pattern Analysis` |
| Task 5 | How many known campaigns has APT-Serpent conducted since 2021? | `4` |
| Task 5 | In which phase of the attack does CustomBackdoor get dropped? | `Execution & Persistence` |
| Task 5 | What is the primary initial access vector used by APT-Serpent? | `Spear-phishing` |
| Task 5 | What is the time interval between CustomBackdoor’s HTTPS C2 beacons? | `300` seconds |
| Task 5 | What is the flag received after choosing the correct threat hunting approach and target? | `THM-APT-SERPENT-INTEL` |

المصدر المرجعي: https://simontaplin.net/2026/07/03/answers-for-the-tryhackme-threat-hunting-introduction-room/

## حالة التحقق داخل المتصفح

تم إدخال جميع الإجابات والتحقق منها داخل غرفة TryHackMe. أظهر المتصفح `Correct Answer` لكل الأسئلة، وكانت إجابات Task 3 وTask 5 كما يلي:

- Task 3، السؤال الأول: `Intelligence-Driven Hunting`
- Task 3، السؤال الثاني: `Indicator-Driven Hunting`
- Task 4: `Attack Residues`
- Task 5، السؤال الأول: `Indicators of Compromise`
- Task 5، السؤال الثاني: `Behavioral Pattern Analysis`
- Task 6: `4`، `Execution & Persistence`، `Spear-phishing`، `300`، `THM-APT-SERPENT-INTEL`
- Task 7: `No answer needed`

ظهرت حالة الغرفة عند النهاية بنسبة تقدم 92% مع ظهور `Correct Answer` في خاتمة الغرفة، وهو نمط TryHackMe المستخدم لإكمال آخر مهمة بعد احتساب المهام السابقة.

## دليل الإكمال النهائي

بعد إكمال Task 7، انتقلت الجلسة إلى صفحة Congratulations وأكدت الرسالة `Great work 9gkc! Room completed!`. أظهرت الصفحة `Completed tasks: 7` و`Points earned: 96`.
