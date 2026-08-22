# الحل النهائي لغرفة Defensive Security Trends

الرابط: [TryHackMe — Defensive Security Trends][1]

## النتيجة

تم حل جميع مهام الغرفة السبع والتحقق من الإجابات مباشرةً في متصفح المستخدم. ظهرت صفحة الإنجاز الرسمية بالعبارة **Great work 9gkc! Room completed!**، مع تسجيل **Completed tasks: 7**.

## جدول الإجابات

| المهمة | السؤال أو المطلوب | الإجابة التي تم التحقق منها |
|---|---|---|
| Task 1 — Introduction | Proceed to the next task | لا توجد إجابة نصية؛ تم الضغط على **Check** |
| Task 2 — Attacks Become Faster | متوسط زمن الوصول إلى الفدية وفق Huntress | `17 hours` |
| Task 2 — Attacks Become Faster | الإجراء المطلوب لتسريع روتين الفرز | `Automate it` |
| Task 3 — Attacks Become Complex | أداة الوصول عن بُعد المستخدمة مع DarkGate | `AnyDesk` |
| Task 3 — Attacks Become Complex | هل أصبح محيط الشبكة أكثر قابلية للتنبؤ؟ | `Nay` |
| Task 4 — Attacks via Valid Accounts | نسبة الحوادث التي تضمنت Valid accounts | `39%` |
| Task 4 — Attacks via Valid Accounts | اسم المجرمين الذين يبيعون الوصول إلى الشبكات | `Initial Access Brokers` |
| Task 5 — Supply Chain Attacks | أول برمجية خبيثة في سلسلة حادثة Vercel | `Lumma Stealer` |
| Task 5 — Supply Chain Attacks | هل تختلف TTPs جوهريًا عن الاختراقات الأخرى؟ | `Nay` |
| Task 6 — AI Impact on Cyber Security | هل ينبغي أن يكون AI صاحب القرار النهائي في SOC؟ | `Nay` |
| Task 6 — AI Impact on Cyber Security | تقنية MITRE التي أصبحت غير صالحة بسبب AI | `None` |
| Task 7 — Research Challenge | إضافة VS Code المخترقة | `Nx Console` |
| Task 7 — Research Challenge | نظام الحزم مفتوح المصدر في جذر سلسلة التوريد | `TanStack` |
| Task 7 — Research Challenge | نمو استخدام RMM سنةً بعد سنة | `240%` |
| Task 7 — Research Challenge | أكثر نوع وصول يبيعه Initial Access Brokers | `VPN` |

## ملاحظات التحقق

تشير إجابات Task 7 إلى أن إصدار **Nx Console 18.95.0** كان الإضافة المخترقة، وأن سلسلة التوريد السابقة ارتبطت بـ **TanStack**. كما يذكر تقرير Verizon 2026 أن استخدام برمجيات RMM نما نسبيًا بنسبة **240%** مقارنةً بالعام السابق، وأن **VPN** مثل النوع الأكثر شيوعًا ضمن عروض الوصول التي يبيعها وسطاء الوصول الأولي.

## المراجع

[1]: https://tryhackme.com/room/defensivesecuritytrends "غرفة Defensive Security Trends على TryHackMe"

[2]: https://github.blog/security/investigating-unauthorized-access-to-githubs-internal-repositories/ "إعلان GitHub حول الوصول غير المصرح به إلى المستودعات الداخلية"

[3]: https://github.com/nrwl/nx-console/security/advisories/GHSA-c9j4-9m59-847w "GitHub Security Advisory — Compromised Nx Console version 18.95.0"

[4]: https://nx.dev/blog/nx-console-v18-95-0-postmortem "Nx Console v18.95.0 supply-chain compromise postmortem"

[5]: https://www.verizon.com/business/resources/T1ae/reports/2026-dbir-data-breach-investigations-report.pdf "Verizon 2026 Data Breach Investigations Report"
