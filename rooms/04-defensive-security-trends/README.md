# Defensive Security Trends — TryHackMe

> **الحالة:** تم إكمال الغرفة والتحقق الرسمي على المنصة. ظهرت رسالة الإنهاء: Great work 9gkc! Room completed! مع إحصائية Completed tasks: 7. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط | [https://tryhackme.com/room/defensivesecuritytrends][1] |
| التصنيف/المجال | Defensive Security |
| الصعوبة | غير مذكورة |
| المدة/المختبر | غير مذكورة |
| عدد المهام | 7 |

## الملخص التنفيذي

تستعرض غرفة Defensive Security Trends أبرز اتجاهات التهديدات الدفاعية: تسارع زمن الوصول إلى الفدية، تعقّد أساليب المهاجمين، الاعتماد المتزايد على الحسابات الصحيحة (Valid accounts)، مخاطر سلسلة التوريد، وتأثير الذكاء الاصطناعي على عمل SOC، مع إنهاء بتحدي بحثي يستند إلى مصادر مفتوحة.

الهدف كان الإجابة عن أسئلة قصيرة والتحقق منها مباشرة داخل TryHackMe. جميع الإجابات أُدخلت وتم قبولها، وأكّدت المنصة اكتمال المهام السبعة.

## مسار الحل

### 1. نظرة عامة على المهام والأسئلة

- Task 1 — Introduction
  - Proceed to the next task: لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً.

- Task 2 — Attacks Become Faster
  - متوسط زمن الوصول إلى الفدية وفق Huntress: تم إدخال القيمة الدقيقة “17 hours”.
  - الإجراء المطلوب لتسريع روتين الفرز: الإجابة “Automate it”.

- Task 3 — Attacks Become Complex
  - أداة الوصول عن بُعد المستخدمة مع DarkGate: “AnyDesk”.
  - هل أصبح محيط الشبكة أكثر قابلية للتنبؤ؟ الإجابة “Nay”.

- Task 4 — Attacks via Valid Accounts
  - نسبة الحوادث التي تضمنت Valid accounts: “39%”.
  - اسم المجرمين الذين يبيعون الوصول إلى الشبكات: “Initial Access Brokers”.

- Task 5 — Supply Chain Attacks
  - أول برمجية خبيثة في سلسلة حادثة Vercel: “Lumma Stealer”.
  - هل تختلف TTPs جوهريًا عن الاختراقات الأخرى؟ الإجابة “Nay”.

- Task 6 — AI Impact on Cyber Security
  - هل ينبغي أن يكون AI صاحب القرار النهائي في SOC؟ “Nay”.
  - تقنية MITRE التي أصبحت غير صالحة بسبب AI: “None”.

- Task 7 — Research Challenge
  - إضافة VS Code المخترقة: “Nx Console”.
  - نظام الحزم مفتوح المصدر في جذر سلسلة التوريد: “TanStack”.
  - نمو استخدام RMM سنةً بعد سنة: “240%”.
  - أكثر نوع وصول يبيعه Initial Access Brokers: “VPN”.

### 2. ملاحظات داعمة مختصرة للمهمة البحثية

- الإضافة المخترقة هي Nx Console، وقد وثّقت المصادر الأمنية حادثة النسخة 18.95.0 تحديدًا كمكوّن متأثر ضمن سلسلة توريد أدوات التطوير [3] [4].
- سلسلة التوريد أشير فيها إلى TanStack كجذر بيئي مفتوح المصدر مرتبط بالسياق المطروح.
- بالنسبة للاتجاهات الصناعية، يورد تقرير Verizon 2026 DBIR نسب نمو لاستخدام أدوات RMM وصلت إلى 240% على أساس سنوي، كما تُذكر VPN كنوع الوصول الأكثر شيوعًا ضمن عروض Initial Access Brokers [5].

## الإجابات النهائية

| المهمة/السؤال | الإجابة المقبولة |
|---|---|
| Task 1 — Introduction — Proceed to the next task | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| Task 2 — Attacks Become Faster — متوسط زمن الوصول إلى الفدية وفق Huntress | `17 hours` |
| Task 2 — Attacks Become Faster — الإجراء المطلوب لتسريع روتين الفرز | `Automate it` |
| Task 3 — Attacks Become Complex — أداة الوصول عن بُعد المستخدمة مع DarkGate | `AnyDesk` |
| Task 3 — Attacks Become Complex — هل أصبح محيط الشبكة أكثر قابلية للتنبؤ؟ | `Nay` |
| Task 4 — Attacks via Valid Accounts — نسبة الحوادث التي تضمنت Valid accounts | `39%` |
| Task 4 — Attacks via Valid Accounts — اسم المجرمين الذين يبيعون الوصول إلى الشبكات | `Initial Access Brokers` |
| Task 5 — Supply Chain Attacks — أول برمجية خبيثة في سلسلة حادثة Vercel | `Lumma Stealer` |
| Task 5 — Supply Chain Attacks — هل تختلف TTPs جوهريًا عن الاختراقات الأخرى؟ | `Nay` |
| Task 6 — AI Impact on Cyber Security — هل ينبغي أن يكون AI صاحب القرار النهائي في SOC؟ | `Nay` |
| Task 6 — AI Impact on Cyber Security — تقنية MITRE التي أصبحت غير صالحة بسبب AI | `None` |
| Task 7 — Research Challenge — إضافة VS Code المخترقة | `Nx Console` |
| Task 7 — Research Challenge — نظام الحزم مفتوح المصدر في جذر سلسلة التوريد | `TanStack` |
| Task 7 — Research Challenge — نمو استخدام RMM سنةً بعد سنة | `240%` |
| Task 7 — Research Challenge — أكثر نوع وصول يبيعه Initial Access Brokers | `VPN` |

## التحقق الرسمي داخل TryHackMe

- إدخال جميع الإجابات تم عبر واجهة المتصفح وقُبلت مباشرة.
- ظهرت رسالة الإتمام الرسمية على لوحة الغرفة: Great work 9gkc! Room completed! مع إحصائية Completed tasks: 7.
- لا توجد إشارة ضمن السياق إلى إرسال تقييم منفصل؛ يقتصر الدليل المرئي على قبول الإجابات وعرض حالة الإكمال.

## الدروس الأمنية

- الأتمتة عنصر حاسم لتسريع الفرز وتقليل زمن الاستجابة، خاصة مع تقليص متوسط زمن الوصول إلى الفدية.
- تعقّد الهجمات يشمل إساءة استخدام أدوات RMM وRAT المشروعة مثل AnyDesk، ما يتطلب مراقبة استخدام الأدوات المصرح بها سياقيًا.
- الحسابات الصحيحة وموفّرو الوصول الأولي يمثلون سطح هجوم رئيسيًا؛ يجب تعزيز الضوابط على الاعتماديات والهويات.
- هجمات سلسلة التوريد تتقاطع مع منظومات الحزم المفتوحة المصدر وإضافات أدوات التطوير؛ يلزم التحقق المتواصل من سلامة السلاسل.
- الذكاء الاصطناعي داعم لعمليات SOC وليس بديلًا عن الحكم البشري؛ لا توجد تقنية MITRE تُعد “غير صالحة” بذاتها بسبب AI.

## المراجع

[1]: https://tryhackme.com/room/defensivesecuritytrends "غرفة Defensive Security Trends على TryHackMe"
[2]: https://github.blog/security/investigating-unauthorized-access-to-githubs-internal-repositories/ "إعلان GitHub حول الوصول غير المصرح به إلى المستودعات الداخلية"
[3]: https://github.com/nrwl/nx-console/security/advisories/GHSA-c9j4-9m59-847w "GitHub Security Advisory — Compromised Nx Console version 18.95.0"
[4]: https://nx.dev/blog/nx-console-v18-95-0-postmortem "Nx Console v18.95.0 supply-chain compromise postmortem"
[5]: https://www.verizon.com/business/resources/T1ae/reports/2026-dbir-data-breach-investigations-report.pdf "Verizon 2026 Data Breach Investigations Report"
