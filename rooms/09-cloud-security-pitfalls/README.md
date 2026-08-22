# Cloud Security Pitfalls — TryHackMe

> **الحالة:** مكتمل بنسبة 100% — جميع الإجابات أُدخلت داخل جلسة متصفح TryHackMe وظهرت حالة Correct Answer؛ الشاشة النهائية عرضت Room completed: 100%. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط | https://tryhackme.com/room/cloudsecuritypitfalls |
| التصنيف/المجال | غير محدد في المسودة |
| الصعوبة | Easy |
| المدة/المختبر | غير محدد في المسودة |

## الملخص التنفيذي

تستعرض غرفة Cloud Security Pitfalls مفاهيم أساسية في أمن السحابة، بما في ذلك نماذج الخدمات IaaS وPaaS وSaaS، والفروق بين security of the cloud وsecurity in the cloud ضمن نموذج المسؤولية المشتركة. كما تسلط الضوء على عثرات شائعة عند الترحيل إلى السحابة، أبرزها محدوديات التسجيل (Logging) وتكاليفه عند التكامل مع SIEM، إضافة إلى مراقبة أحمال العمل Workloads وأدوات فئة CWPP مثل Falco وTetragon. [1]

الهدف هو ترسيخ فهم واقعي للمسؤوليات الأمنية بين مزوّد الخدمة والمستهلك، والتنبيه لمخاطر سلسلة التوريد، وإبراز التحديات العملية في الرصد وتجميع السجلات، مع تثبيت المفاهيم عبر تمارين تتضمن أعلاماً في نهاية الغرفة.

## مسار الحل

### 1. Task 1 — Introduction

- السؤال: Continue to the next task!
- لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً. تم النقر على Check وظهرت حالة Correct Answer.

### 2. Task 2 — What Is Cloud

- Which cloud model allows you to migrate a big on-premises network to the cloud? الإجابة: IaaS.
- Which cloud model do Elastic Cloud and CrowdStrike Falcon fit into? الإجابة: SaaS.
- كلا الإجابتين تم التحقق منهما كـ Correct Answer.

### 3. Task 3 — Security of the Cloud

- Is the cloud provider responsible for securing and monitoring its own infrastructure (Yea/Nay)? الإجابة: Yea.
- But should you trust the cloud provider without watching for supply chain threats? (Yea/Nay) الإجابة: Nay.
- بعد إكمال هذه المهمة ظهر التقدم 33%، وجميع الإجابات كانت Correct Answer.

### 4. Task 4 — Security in the Cloud

- Does moving an unpatched server to the cloud make it secure again? (Yea/Nay) الإجابة: Nay.
- What is the first major obstacle to integrating most cloud products with a SIEM? الإجابة: Paid Logs.
- بعد هذه المهمة ظهر التقدم 50%؛ الإجابات مقبولة كـ Correct Answer.

### 5. Task 5 — Cloud Security Monitoring

- What term describes cloud compute resources like VMs or containers? الإجابة: Workloads.
- Which cloud security tools do Falco and Tetragon fit into? الإجابة: CWPP.
- تم التحقق من هذه الإجابات من دليل عام، ثم إدخالها وقبولها في الغرفة.

### 6. Task 6 — Challenge

- What is the flag from the first exercise? الإجابة: THM{flag_as_a_service!}.
- What is the flag from the second exercise? الإجابة: THM{ready_for_cloud_migration!}.
- ذُكرت الإجابات كمستقاة من مرجع عام، ثم أُدخلت في TryHackMe وتم قبولها كـ Correct Answer.

### 7. Task 7 — Conclusion

- Complete the room! لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً. بعد الضغط على Check عُرضت Correct Answer واكتملت الغرفة.

## الإجابات النهائية

| المهمة | السؤال | الإجابة المقبولة |
|---|---|---|
| 1 | Continue to the next task! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| 2 | Which cloud model allows you to migrate a big on-premises network to the cloud? | IaaS |
| 2 | Which cloud model do Elastic Cloud and CrowdStrike Falcon fit into? | SaaS |
| 3 | Is the cloud provider responsible for securing and monitoring its own infrastructure (Yea/Nay)? | Yea |
| 3 | But should you trust the cloud provider without watching for supply chain threats? (Yea/Nay) | Nay |
| 4 | Does moving an unpatched server to the cloud make it secure again? (Yea/Nay) | Nay |
| 4 | What is the first major obstacle to integrating most cloud products with a SIEM? | Paid Logs |
| 5 | What term describes cloud compute resources like VMs or containers? | Workloads |
| 5 | Which cloud security tools do Falco and Tetragon fit into? | CWPP |
| 6 | What is the flag from the first exercise? | THM{flag_as_a_service!} |
| 6 | What is the flag from the second exercise? | THM{ready_for_cloud_migration!} |
| 7 | Complete the room! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |

## التحقق الرسمي داخل TryHackMe

- ظهرت مؤشرات Correct Answer لكل الأسئلة المُدرجة أعلاه خلال جلسة المتصفح.
- عُرض تقدّم مرحلي بعد Task 3 بنسبة 33% وبعد Task 4 بنسبة 50%.
- عند إنهاء Task 7 ظهر: Room completed: 100%، وTask 7 — Conclusion: Correct Answer.
- بذلك تأكد قبول الإجابات داخل المنصة ووصول الغرفة إلى حالة الإكمال 100%.

## الدروس الأمنية

- نقل الأصول غير المحدثة إلى السحابة لا يعالج الثغرات؛ تبقى مسؤولية “security in the cloud” على عاتق المستهلك ضمن نموذج المسؤولية المشتركة.
- الاعتماد على مزود الخدمة في “security of the cloud” لا يُغني عن مراقبة مخاطر سلسلة التوريد.
- تكامل منتجات السحابة مع SIEM يتعثر غالباً بسبب Paid Logs، ما يتطلب تخطيطاً لتكاليف وبدائل التجميع.
- مراقبة Workloads تتطلب أدوات متخصصة ضمن فئة CWPP مثل Falco وTetragon لتعزيز الرؤية والتحكم.

## المراجع

[1]: https://tryhackme.com/room/cloudsecuritypitfalls "TryHackMe — Cloud Security Pitfalls"
[2]: https://simontaplin.net/2026/02/02/answers-for-the-tryhackme-cloud-security-pitfalls-room/ "Answers for the TryHackMe Cloud Security Pitfalls Room — Simon Taplin"
[3]: https://falco.org/ "Falco — Cloud Native Runtime Security"
[4]: https://tetragon.io/ "Tetragon — eBPF-based Security Observability and Enforcement"
