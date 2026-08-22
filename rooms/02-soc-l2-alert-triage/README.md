# SOC L2 Alert Triage — TryHackMe

> **الحالة:** تم الإكمال الرسمي داخل المنصة؛ تظهر على صفحة الغرفة عبارة Room completed: 100% [1]. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| البند | القيمة |
|---|---|
| رابط الغرفة | https://tryhackme.com/room/socl2alerttriage |
| التصنيف/المجال | لم يُذكر في المسودة |
| الصعوبة | Easy |
| المدة | 45 min |

## الملخص التنفيذي

تغطي غرفة SOC L2 Alert Triage منهجية فرز التنبيهات على مستوى L2 بدءاً من فهم سياق التنبيه، مروراً بتحليل السجلات وبناء Timeline للهجوم، وصولاً إلى قرارات الاستجابة والتعافي والدروس المستفادة. يتدرّب المتعلم على تحديد محفّزات البدء بـ triage، وضبط الحكم على صحة التنبيه، واتخاذ إجراءات استجابة مناسبة عند غياب تأكيد من Red Team.

تتضمن الغرفة تحدياً عملياً عبر تطبيق ويب ثابت يساعد على تصنيف خطوات التحليل، ترتيب إجراءات الاستجابة، واستخراج العلم النهائي الذي يؤكد إتمام مراحل التحليل والاستجابة بنجاح.

## مسار الحل

### 1. الانضمام وبداية المهام

- تم الانضمام للغرفة وفتح المهام بالترتيب: Task 1 Introduction، Task 2 SOC L2 Workflow، Task 3 Log Analysis as L2، Task 4 Threat Response، Task 5 Learning Lessons، Task 6 Conclusion.
- Task 1 لا يتطلب إجابة وتم تأكيده عبر زر Check.

### 2. Task 2 — SOC L2 Workflow

- السؤال: What is the most common trigger for L2 to start the triage?
- وفق محتوى الغرفة، المُحفّز الشائع هو تنبيه SOC مُصعَّد.
- الإجابة المقبولة: Escalated alert.

### 3. Task 3 — Log Analysis as L2

- السؤال 1: Should you understand the rule purpose before triaging the alert? (Yea/Nay)
  - الإجابة المقبولة: Yea.
- السؤال 2: What term is used for a chronological list of events related to the attack?
  - الإجابة المقبولة: Timeline.

### 4. Task 4 — Threat Response

- السؤال 1: What is the term for a temporary response that stops the threat from spreading?
  - الإجابة المقبولة: Containment.
- السؤال 2: You see a clearly malicious activity on one of the corporate devices. You also know about an ongoing pentest, but red teamers do not respond. Would you isolate the device before receiving a confirmation? (Yea/Nay)
  - الإجابة المقبولة: Yea.

### 5. Task 5 — Learning Lessons (التطبيق العملي)

- تم فتح تطبيق الويب المرتبط بالمهمة: https://static-labs.tryhackme.cloud/apps/soc-l2-alert-triage/ [2].
- مراحل التطبيق:
  1) Alert Analysis — تصنيف البطاقات:
     - SEE WHAT HAPPENED:
       - Check the past activity: who launched Claude and where it was downloaded from
       - Quickly review what the malware is doing now and how urgent the situation is
     - BUILD A TIMELINE:
       - Trace and note the malware's full process, file, and network activity up to the present time
       - Reconstruct the complete attack timeline and collect indicators of compromise (IOCs)
     - MAKE YOUR VERDICT:
       - Determine the root cause of Claude running malware: supply chain, prompt injection, or an imposter binary
       - Reach a True Positive verdict and proceed to the Response stage with the collected IOCs
  2) Response Actions — الترتيب الصحيح:
     - Isolate the infected LPT-1601 from the network
     - Rotate all stolen passwords, keys, and tokens
     - Eradicate the infostealer and its files from the host
     - Lift host isolation and inform the user and your team
  3) Lessons Learned — تُحدَّد من داخل التطبيق بعد الاستجابة.

- تضمّن منطق JavaScript في التطبيق قيمة العلم بصيغة Base64:
```
VEhNe3RyaWFnZV9kb25lX3JpZ2h0IX0=
```
- القيمة بعد فك الترميز:
```
THM{triage_done_right!}
```
- تم إدخال العلم في سؤال Task 5 وقُبلت الإجابة.

### 6. Task 6 — Conclusion

- لا توجد إجابة مطلوبة؛ تم تأكيد المهمة عبر زر Check لإغلاق الغرفة بعد إكمال المهام السابقة.

## الإجابات النهائية

| المهمة | السؤال أو المطلوب | الإجابة المقبولة |
|---|---|---|
| Task 1 — Introduction | لا توجد إجابة مطلوبة | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| Task 2 — SOC L2 Workflow | What is the most common trigger for L2 to start the triage? | Escalated alert |
| Task 3 — Log Analysis as L2 | Should you understand the rule purpose before triaging the alert? | Yea |
| Task 3 — Log Analysis as L2 | What term is used for a chronological list of events related to the attack? | Timeline |
| Task 4 — Threat Response | What is the term for a temporary response that stops the threat from spreading? | Containment |
| Task 4 — Threat Response | Would you isolate the device before receiving confirmation from the red team? | Yea |
| Task 5 — Learning Lessons | What is the flag you get at the end of the challenge? | THM{triage_done_right!} |
| Task 6 — Conclusion | Complete the room! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |

## التحقق الرسمي داخل TryHackMe

- تم إدخال الإجابات والتحقق منها عبر أزرار Check لكل مهمة داخل الغرفة، بما في ذلك إدخال العلم النهائي في Task 5.
- عُرضت على صفحة الغرفة عبارة Room completed: 100% تأكيداً لإتمام الحل [1].
- لا توجد إشارة في المسودة إلى إرسال تقييم منفصل؛ يقتصر التحقق على قبول الإجابات داخل المنصة.

## الدروس الأمنية

- يبرز المسار أهمية فهم هدف القاعدة قبل فرز التنبيه، وبناء Timeline زمني شامل مدعوم بـ IOCs لاتخاذ قرار True Positive. كما يؤكد على أولوية الاحتواء السريع عند رصد نشاط خبيث مؤكّد حتى بوجود اختبار اختراق جارٍ دون تأكيد فوري. تُرتَّب إجراءات الاستجابة بدءاً من العزل، مروراً بتدوير الأسرار، ثم الاستئصال، وأخيراً إعادة الدمج والتواصل.

## المراجع

[1]: https://tryhackme.com/room/socl2alerttriage "TryHackMe — SOC L2 Alert Triage"
[2]: https://static-labs.tryhackme.cloud/apps/soc-l2-alert-triage/ "TryHackMe Static Challenge — SOC L2 Alert Triage"
