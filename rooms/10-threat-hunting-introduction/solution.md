# TryHackMe — Threat Hunting: Introduction

**Room:** [Threat Hunting: Introduction](https://tryhackme.com/room/threathuntingintroduction)  
**Difficulty:** Easy  
**Status:** **Completed**

تم إدخال الإجابات والتحقق منها داخل متصفح المستخدم. ظهرت عبارة **Correct Answer** لكل سؤال، بما في ذلك سؤال الخاتمة.

## Answers

| Task | Question | Answer |
|---|---|---|
| 1 | I am ready to start! | No answer needed; Check completed |
| 2 | What is the average number of days an attacker remains undetected in a network called? | `Dwell time` |
| 2 | Is threat hunting reactive or proactive? | `Proactive` |
| 3 | Which threat hunting approach would you use if you have received threat intelligence about an APT group targeting your industry? | `Intelligence-Driven Hunting` |
| 3 | Which threat hunting approach is most efficient when you have a list of file hashes and IOCs from a threat feed? | `Indicator-Driven Hunting` |
| 4 | What category of hunting target represents artifacts left behind by attackers during their attack? | `Attack Residues` |
| 5 | Which hunting technique uses file hashes, IP addresses, and domain names to search for specific artifacts? | `Indicators of Compromise` |
| 5 | What hunting technique is represented by “Word.exe spawns cmd.exe spawns powershell.exe that connects to external IP”? | `Behavioral Pattern Analysis` |
| 6 | How many known campaigns has APT-Serpent conducted since 2021? | `4` |
| 6 | In which phase of the attack does CustomBackdoor get dropped? | `Execution & Persistence` |
| 6 | What is the primary initial access vector used by APT-Serpent? | `Spear-phishing` |
| 6 | What is the time interval between CustomBackdoor’s HTTPS C2 beacons? | `300` seconds |
| 6 | What is the flag received after choosing the correct threat hunting approach and target? | `THM-APT-SERPENT-INTEL` |
| 7 | Great work! You are now ready for the next room: Threat Hunting: Foothold. | No answer needed; Check completed |

## Concepts Covered

تتناول الغرفة الفرق بين **Threat Hunting** و**Incident Response**، حيث يعتمد صيد التهديدات على البحث الاستباقي، بينما تستجيب الاستجابة للحوادث عادةً لتنبيه أو حادث مؤكد. كما تشرح مفهوم **Dwell Time**، وأساليب الصيد المبني على الفرضية والذكاء والمؤشرات، وأهداف الصيد مثل البرمجيات الخبيثة المعروفة وآثار الهجوم والثغرات المعروفة.

وتشمل تقنيات الصيد التي تمت مراجعتها **Attack Signatures** و**Indicators of Compromise** و**Behavioral Pattern Analysis** و**Logical Queries and Anomaly Detection**. أما الجزء العملي فطبّق هذه المفاهيم على معلومات استخباراتية تخص APT-Serpent وCustomBackdoor.

## Verification

أظهر متصفح TryHackMe في نهاية الغرفة حالة سؤال Task 7 على النحو التالي:

> Correct Answer

كما ظهرت المهام السابقة بعلامة الإكمال الخضراء، وتم التحقق من جميع الإجابات داخل الغرفة.

## References

[1]: https://tryhackme.com/room/threathuntingintroduction "TryHackMe — Threat Hunting: Introduction"
[2]: https://simontaplin.net/2026/07/03/answers-for-the-tryhackme-threat-hunting-introduction-room/ "Answers for the TryHackMe Threat Hunting: Introduction Room — Simon Taplin"
[3]: https://attack.mitre.org/ "MITRE ATT&CK"

## Final Completion Evidence

بعد التحقق النهائي، انتقلت الجلسة إلى صفحة Congratulations وأكدت الرسالة:

> Great work 9gkc! Room completed!

كما أظهرت الصفحة `Completed tasks: 7` و`Points earned: 96`.
