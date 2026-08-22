# Threat Hunting: Introduction — TryHackMe

> **الحالة:** الغرفة مكتملة رسمياً داخل TryHackMe؛ تم إدخال الإجابات والتحقق منها جميعاً مع ظهور عبارة “Correct Answer” في كل الأسئلة، وتظهر صفحة التهاني برسالة “Great work 9gkc! Room completed!” مع “Completed tasks: 7” و“Points earned: 96”. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| الرابط | التصنيف/المجال | الصعوبة | المدة/المختبر |
|---|---|---|---|
| https://tryhackme.com/room/threathuntingintroduction | Threat Hunting | Easy | — |

## الملخص التنفيذي

تقدّم غرفة Threat Hunting: Introduction مدخلاً منظماً لمفاهيم صيد التهديدات، والفروق العملية بينه وبين Incident Response، مع التركيز على دور الصيد الاستباقي في كشف النشاطات الخبيثة التي قد تمر دون ملاحظة لفترات طويلة (Dwell time). تغطي الغرفة مناهج الصيد الأساسية: Hypothesis-Driven، Intelligence-Driven، وIndicator-Driven، وأهداف الصيد مثل البرمجيات الخبيثة المعروفة، وآثار الهجوم (Attack Residues)، والثغرات/العيوب المعروفة. [1]

تتدرج المهام لربط المفاهيم بالتقنيات العملية: Attack Signatures، Indicators of Compromise، Behavioral Pattern Analysis، وLogical Queries and Anomaly Detection. وفي الشق التطبيقي، تُوظَّف معلومات استخباراتية عن APT-Serpent وملف CustomBackdoor لاختيار النهج والهدف المناسبين، وصولاً إلى تحصيل العلم (flag) المطلوب.

## مسار الحل

### 1. مبادئ الصيد وأساليبه

- ترسيخ التعريف بـ Dwell time بوصفه متوسط مدة بقاء المهاجم دون اكتشاف داخل الشبكة، وتأكيد الطبيعة الاستباقية لصيد التهديدات مقارنة برد الفعل في Incident Response.
- تمييز مناهج الصيد:
  - Intelligence-Driven Hunting عند توافر Threat Intelligence حول APT يستهدف القطاع.
  - Indicator-Driven Hunting عند توافر قوائم مؤشرات اختراق وملفات Hash من Threat Feeds.

### 2. أهداف وتقنيات الصيد

- تحديد “Attack Residues” كفئة تمثل الآثار/المخلّفات التي يتركها المهاجمون أثناء هجماتهم.
- تطبيق تقنيات الصيد:
  - Indicators of Compromise للاعتماد على مؤشرات كعناوين IP وأسماء النطاقات وملفات Hash للبحث عن قطعية أدلة محددة.
  - Behavioral Pattern Analysis لتحليل تسلسل سلوكي مثل: “Word.exe spawns cmd.exe spawns powershell.exe that connects to external IP”.

### 3. تطبيق استخباراتي على APT-Serpent

- الاستناد إلى المعطيات الاستخباراتية حول APT-Serpent:
  - عدد الحملات منذ 2021، طور إسقاط CustomBackdoor، متجه الوصول الأولي (Initial Access Vector)، وفاصل نبضات C2 عبر HTTPS.
- اختيار النهج المناسب (Intelligence-Driven Hunting) مع الهدف الملائم للصيد طبقاً للمعطيات، ما أفضى إلى إظهار العلم: THM-APT-SERPENT-INTEL.

## الإجابات النهائية

| المهمة/السؤال | الإجابة المقبولة |
|---|---|
| Task 1 — I am ready to start! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| Task 2 — What is the average number of days an attacker remains undetected in a network called? | `Dwell time` |
| Task 2 — Is threat hunting reactive or proactive? | `Proactive` |
| Task 3 — Which threat hunting approach would you use if you have received threat intelligence about an APT group targeting your industry? | `Intelligence-Driven Hunting` |
| Task 3 — Which threat hunting approach is most efficient when you have a list of file hashes and IOCs from a threat feed? | `Indicator-Driven Hunting` |
| Task 4 — What category of hunting target represents artifacts left behind by attackers during their attack? | `Attack Residues` |
| Task 5 — Which hunting technique uses file hashes, IP addresses, and domain names to search for specific artifacts? | `Indicators of Compromise` |
| Task 5 — What hunting technique is represented by “Word.exe spawns cmd.exe spawns powershell.exe that connects to external IP”? | `Behavioral Pattern Analysis` |
| Task 6 — How many known campaigns has APT-Serpent conducted since 2021? | `4` |
| Task 6 — In which phase of the attack does CustomBackdoor get dropped? | `Execution & Persistence` |
| Task 6 — What is the primary initial access vector used by APT-Serpent? | `Spear-phishing` |
| Task 6 — What is the time interval between CustomBackdoor’s HTTPS C2 beacons? | `300` seconds |
| Task 6 — What is the flag received after choosing the correct threat hunting approach and target? | `THM-APT-SERPENT-INTEL` |
| Task 7 — Great work! You are now ready for the next room: Threat Hunting: Foothold. | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |

## التحقق الرسمي داخل TryHackMe

- قبول الإجابات: ظهرت عبارة “Correct Answer” على جميع أسئلة الغرفة، بما في ذلك سؤال الخاتمة.
- دليل الإكمال: بعد إتمام آخر مهمة، ظهرت صفحة التهاني برسالة “Great work 9gkc! Room completed!”، كما عُرضت مؤشرات الإكمال “Completed tasks: 7” و“Points earned: 96”.
- لا توجد ملاحظات تخص إرسال تقييم؛ التحقق تم كاملاً داخل واجهة الغرفة.

## الدروس الأمنية

- توظيف Threat Intelligence يرفع كفاءة الصيد عند استهدافات APT محددة، بينما تُستثمر مؤشرات الاختراق في عمليات تمشيط واسعة وسريعة.
- الجمع بين IOCs وتحليل الأنماط السلوكية يعزز القدرة على رصد الأنشطة الخبيثة التي تتجاوز التطابقات التوقيعية التقليدية، خاصةً عند وجود تسلسل عمليات مشبوه واتصالات خارجية.
- تقليل Dwell time يتطلب صيداً استباقياً مستمراً يركز على Attack Residues ومراقبة قنوات C2 وفواصل النبضات المميزة للبرمجيات الخبيثة.

## المراجع

[1]: https://tryhackme.com/room/threathuntingintroduction "TryHackMe — Threat Hunting: Introduction"
[2]: https://simontaplin.net/2026/07/03/answers-for-the-tryhackme-threat-hunting-introduction-room/ "Answers for the TryHackMe Threat Hunting: Introduction Room — Simon Taplin"
[3]: https://attack.mitre.org/ "MITRE ATT&CK"
