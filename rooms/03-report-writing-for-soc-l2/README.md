# Report Writing for SOC L2 — TryHackMe

> **الحالة:** تم إكمال الغرفة بنجاح؛ ظهرت داخل الواجهة العبارة Room completed: 100%، وتم اعتماد جميع الإجابات والأعلام. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط | https://tryhackme.com/room/reportwritingsocl2 |
| التصنيف/المجال | غير مذكور |
| الصعوبة | غير مذكور |
| المدة | غير مذكور |
| المختبر/التطبيق التفاعلي | https://static-labs.tryhackme.cloud/apps/soc-l2-report-dfir/ |

## الملخص التنفيذي

تتناول الغرفة Report Writing for SOC L2 مهارات التواصل والتقرير لدى محلل L2 في بيئة SOC، بما يشمل التفريق بين أدوار L1 وL2 في الربط مع العالم الخارجي، وصياغة تواصل قيادي واضح ومهني، وإعداد DFIR handover notes فعّالة ودقيقة زمنياً، إضافة إلى مبادئ الاستخدام المسؤول للذكاء الاصطناعي في كتابة التقارير. [1]

الهدف هو تصنيف العيوب الاتصالية ضمن تحديات تفاعلية، تقديم إجابات مباشرة على أسئلة نظرية، والحصول على أعلام تثبت اجتياز التحديات. تم اعتماد الإجابات كافة، وحُصل على الأعلام المطلوبة كما وردت في واجهة الغرفة.

## مسار الحل

### 1. Task 1 — Introduction

- السؤال “Let's go!” لا يتطلب إدخال نصي؛ تم تأكيد المهمة عبر Check.
- المؤشر المرئي للتقدم بعد الإكمال: 8%.

### 2. Task 2 — L1 vs L2 Communication

- أي مستوى يربط SOC بالعالم الخارجي؟ الإجابة: `L2`.
- ماذا يكتب محللو L2 لتلخيص نتائج SOC؟ الإجابة: `Reports`.
- تم التحقق من الإجابتين، وارتفع التقدم إلى 25%.

### 3. Task 3 — Leadership Communication

- التحدي التفاعلي C-Level Communication أُنجز بنتيجة 5/5، وظهر العلم: `THM{executive_summary_approved}`.
- الإجابات النظرية:
  - Should you complete the analysis after sharing the initial SOC report? الإجابة: `Yea`.
  - Should you keep your team informed about the ongoing communication? الإجابة: `Yea`.

تصنيفات الأجزاء المظللة ضمن التحدي كانت كما يلي:

| النص المظلل/العنصر | التصنيف |
|---|---|
| الجزء المتعلق بغياب المستلم | `Missing recipient` |
| الجزء المتعلق بغياب السياق | `Missing context` |
| الرد المفرط | `Excessive response` |
| الجدول الزمني غير الواضح | `Unclear timeline` |
| اللغة غير المهنية | `Unprofessional language` |

### 4. Task 4 — SOC/DFIR Communication

- Are L2 handover notes meant for a non-technical audience? الإجابة: `Nay`.
- What part of the handover notes lists your findings chronologically? الإجابة: `Attack Timeline`.
- التحدي التفاعلي (DFIR handover) عبر التطبيق: https://static-labs.tryhackme.cloud/apps/soc-l2-report-dfir/ نتج عنه العلم: `THM{trysaveme_would_be_proud}`.

تصنيفات الأجزاء المظللة ضمن DFIR كانت كما يلي:

| النص أو العنصر المظلل | التصنيف |
|---|---|
| `but given the overall nature of the circumstances surrounding the incident` | `Unnecessary text` |
| `OT environment may have been affected in some way` | `Ambiguous phrasing` |
| `was executed` | `Missing actor` |
| `was exfiltrated` | `No evidence` |
| `Other IPs` | `Missing context` |

- المؤشر المرئي للتقدم بعد إكمال المهمة: 50%.

### 5. Task 5 — Responsible AI Usage

- What should be provided in the AI prompt to get the best reports? الإجابة: `Context`.
- Should you fully rely on GenAI for critical decision-making? الإجابة: `Nay`.
- تم قبول الإجابتين.

### 6. Task 6 — Conclusion

- لا تتطلب إدخال نصي؛ تم تأكيد المهمة عبر Check.
- الحالة النهائية المعروضة: Room completed: 100%.

## الإجابات النهائية

| المهمة/السؤال | الإجابة المقبولة |
|---|---|
| Task 1 — Introduction: تأكيد بدء الغرفة | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| Task 2 — L1 vs L2 Communication: ما المستوى الذي يربط SOC بالعالم الخارجي؟ | `L2` |
| Task 2 — L1 vs L2 Communication: ماذا يكتب محللو L2 لتلخيص نتائج SOC؟ | `Reports` |
| Task 3 — Leadership Communication: Should you complete the analysis after sharing the initial SOC report? | `Yea` |
| Task 3 — Leadership Communication: Should you keep your team informed about the ongoing communication? | `Yea` |
| Task 3 — Leadership Communication: Flag | `THM{executive_summary_approved}` |
| Task 4 — SOC/DFIR Communication: Are L2 handover notes meant for a non-technical audience? | `Nay` |
| Task 4 — SOC/DFIR Communication: What part of the handover notes lists your findings chronologically? | `Attack Timeline` |
| Task 4 — SOC/DFIR Communication: Flag | `THM{trysaveme_would_be_proud}` |
| Task 5 — Responsible AI Usage: What should be provided in the AI prompt to get the best reports? | `Context` |
| Task 5 — Responsible AI Usage: Should you fully rely on GenAI for critical decision-making? | `Nay` |
| Task 6 — Conclusion: إكمال الغرفة | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |

## التحقق الرسمي داخل TryHackMe

- مؤشرات مرئية مؤكِّدة:
  - بعد Task 1: تقدّم 8%.
  - بعد Task 2: تقدّم 25%.
  - بعد Task 4: تقدّم 50%.
  - في نهاية الغرفة: Room completed: 100%.
- قبول الإجابات:
  - جميع إجابات المهام التأكيدية والأسئلة النظرية قبلتها المنصة، وظهرت نتيجة 5/5 في تحدي C-Level Communication.
  - الأعلام ظهرت نصاً داخل التحديات كما يلي: `THM{executive_summary_approved}` و`THM{trysaveme_would_be_proud}`.
- الإرسال/التقييم:
  - جميع الإجابات أُرسلت وتم اعتمادها داخل المنصة؛ لا توجد إجابات معلّقة أو غير مُرسلة.

## الدروس الأمنية

- فعالية تقارير L2 تتطلب تحديد الجمهور بدقة، واقتصار النص على ما تدعمه الأدلة، مع سرد زمني واضح للهجمات عبر Attack Timeline، وتجنّب الغموض واللغة غير المهنية.
- التواصل القيادي يستلزم متابعة التحقيق بعد التقرير الأولي وإبقاء الفريق على اطلاع مستمر، مع توثيق مختصر وواضح قابل للتنفيذ.
- الاستخدام المسؤول لـ GenAI يعتمد على تزويده بالسياق المناسب والتحقق البشري النهائي، وتجنّب الاعتماد الكامل عليه في القرارات الحرجة.

## المراجع

[1]: https://tryhackme.com/room/reportwritingsocl2
[2]: https://static-labs.tryhackme.cloud/apps/soc-l2-report-dfir/
