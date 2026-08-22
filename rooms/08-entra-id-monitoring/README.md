# Entra ID Monitoring — TryHackMe

> **الحالة:** الغرفة مكتملة. تم إدخال جميع الإجابات والتحقق منها داخل متصفح TryHackMe كـ Correct Answer. ظهرت صفحة الإكمال النهائية تؤكد إتمام 7 مهام والحصول على 80 نقطة، مع تشغيل المختبر EntraID-Monitoring-v1 خلال الجلسة. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط | [Entra ID Monitoring][1] |
| المختبر | EntraID-Monitoring-v1 (عنوان IP خلال الجلسة: 10.48.150.192) |

## الملخص التنفيذي

تغطي الغرفة مراقبة Entra ID عبر سيناريو متكامل يبدأ بهجمات Password Spraying وThrottled Brute Force، مروراً برصد Risky Sign-ins وتفعيل سياسات Conditional Access، ثم تحليل هجمات MFA Fatigue وأساليب تجاوزها، ويتصاعد إلى Privilege Escalation وPersistence من خلال إنشاء حساب بامتيازات عالية وإضافة جهاز MFA جديد، وينتهي بإساءة استخدام تطبيقات OAuth ومنح أذونات عالية الحساسية مثل Mail.Read.All.

أُنجزت المهام وفق أدلة السجلات المتاحة في المختبر، وتضمنت التعرف على عناوين IP الخبيثة، تحديد المستخدمين المعرضين للخطر ونوع المخاطر، مخرجات CAP التي منعت محاولات تسجيل الدخول، وتواريخ/أوقات نجاح المهاجم وخطوات ما بعد الاختراق.

## مسار الحل

### 1. Task 1 — Introduction

- السؤال Ready to learn!: لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً.
- تم الضغط على Check وتم قبول الحالة كـ Correct Answer.

ملاحظة المختبر:
- تم تشغيل Lab Machine باسم EntraID-Monitoring-v1. تغيّر عنوان IP أثناء الجلسة من 10.48.145.192 إلى 10.48.150.192، وتم استخدام رابط المختبر من صفحة الغرفة.

### 2. Task 2 — Password-Based Attacks

- تم استخدام الاستعلام التالي كما ورد في الغرفة لتصفية محاولات تسجيل الدخول الفاشلة ذات صلة بالهجمات القائمة على كلمة المرور:
```
index="task-2" sourcetype="azure:aad:signin" "status.errorCode"!=0 conditionalAccessStatus!=success
```
- النتائج الداعمة:
  - عنوان IP لهجوم Password Spraying: 94.20.222.248.
  - عنوان IP لهجوم Throttling Brute Force: 38.165.231.218.
  - البريد الإلكتروني للحساب المخترق: amanda.costa@finegalo.thm.
- جميع الإجابات اعتُمِدت كـ Correct Answer.

### 3. Task 3 — Conditional Access Policies & Identity Protection

- المستخدم المعرض للخطر: allan.senna@finegalo.thm.
- آخر محاولة Risky Sign-in وفق سجلات Risk Detection: 2026-03-03 13:51.
- نوع الخطر المكتشف: anonymizedIPAddress.
- سياسة CAP المطبَّقة التي منعت بعض المحاولات: Block Suspicious Countries.
- عنوان IP الذي مُنع من تسجيل الدخول لذلك المستخدم: 94.20.222.251.
- جميع الإجابات اعتُمِدت كـ Correct Answer.
- تقدم التحدي بعد هذه المهمة: 47%.

### 4. Task 4 — MFA Bypass Techniques

- هدف هجوم MFA fatigue: igor.bicalho@finegalo.thm.
- رمز الخطأ لمحاولات MFA الفاشلة: 500121.
- رمز الدولة المعتاد لتسجيل دخول المستخدم قبل الهجوم: DK.
- توقيت نجاح مصادقة المهاجم: 2026-03-04 13:26.
- جميع الإجابات اعتُمِدت كـ Correct Answer.
- تقدم التحدي بعد هذه المهمة: 68%.

### 5. Task 5 — Privilege Escalation & Persistence

- البريد الإلكتروني للحساب الذي أنشأه المهاجم: rafael.maciel@finegalo.thm.
- الدور المعيّن للحساب الجديد (Role.DisplayName): Global Administrator.
- توقيت إضافة جهاز MFA جديد: 2026-03-04 13:36.
- جميع الإجابات اعتُمِدت كـ Correct Answer.
- تقدم التحدي بعد هذه المهمة: 78%.

### 6. Task 6 — OAuth Application Abuse

- الإذن الذي يسمح بقراءة جميع صناديق البريد في المستأجر: Mail.Read.All.
- قيمة activityDisplayName لتتبع منح الموافقات للتطبيقات في سجلات Entra ID: Consent to application.
- الإجابتان اعتُمِدتا كـ Correct Answer.
- تقدم التحدي بعد هذه المهمة: 94%.

### 7. Task 7 — Conclusion

- السؤال Ready for Exchange Online Monitoring room!: لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً.
- تم الضغط على Check ثم ظهرت صفحة التهنئة مكتملة (Room completed! Completed tasks: 7. Points earned: 80) كما في [صفحة الإكمال النهائية][3].

## الإجابات النهائية

| المهمة | السؤال | الإجابة |
|---|---|---|
| 1 | Ready to learn! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| 2 | Which IP address is performing a password spraying? | 94.20.222.248 |
| 2 | Which IP address is performing a throttling brute force? | 38.165.231.218 |
| 2 | What is the user's email address that was compromised? | amanda.costa@finegalo.thm |
| 3 | What is the user email address that is at risk in the tenant? | allan.senna@finegalo.thm |
| 3 | When was the last risky sign-in attempt from this risky user based on risk detection logs? | 2026-03-03 13:51 |
| 3 | What is the type of risk identified during this risky user sign-in based on risk detection logs? | anonymizedIPAddress |
| 3 | What is the name of the CAP policy that was enforced and blocked some sign-in attempts from this risky user? | Block Suspicious Countries |
| 3 | What was the IP address that was blocked from signing in this risky user? | 94.20.222.251 |
| 4 | Which user was the target of an MFA fatigue attack? | igor.bicalho@finegalo.thm |
| 4 | What is the error code of the failed MFA prompts? | 500121 |
| 4 | What is the country code that the user normally signs in before the attack? | DK |
| 4 | When does the attacker successfully authenticate in the user account? | 2026-03-04 13:26 |
| 5 | What is the user email address that the attacker created? | rafael.maciel@finegalo.thm |
| 5 | Which role (Role.DisplayName) was assigned to this new account? | Global Administrator |
| 5 | When did the attacker add a new MFA device? | 2026-03-04 13:36 |
| 6 | Which permission allows an application to read all mailboxes within a tenant? | Mail.Read.All |
| 6 | What is the activityDisplayName value used to track all consent grants to applications within Entra ID audit logs? | Consent to application |
| 7 | Ready for Exchange Online Monitoring room! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |

## التحقق الرسمي داخل TryHackMe

- تم عرض شارة Correct Answer لكل سؤال تم إدخاله عبر واجهة المتصفح.
- عند إتمام Task 7، عُرضت صفحة الإكمال النهائية تتضمن الرسالة: “Great work 9gkc! Room completed! Completed tasks: 7. Points earned: 80.” مع رابط الصفحة النهائية للإكمال [3].
- لم تُعرض معلومات إضافية عن التقييم داخل الغرفة بخلاف قبول الإجابات وإتمام المهام.

## الدروس الأمنية

- رصد وتحليل أنماط محاولات تسجيل الدخول الفاشلة يمكّن من تمييز Password Spraying وThrottled Brute Force مبكراً وقطع سلسلة الهجوم.
- تفعيل سياسات Conditional Access واستثمار قدرات Identity Protection يسهمان في منع محاولات تسجيل الدخول عالية المخاطر، خاصة من عناوين IP مجهولة أو دول مشبوهة.
- التوعية بمخاطر MFA fatigue وتطبيق ضوابط مثل رقم المطابقة أو تنبيهات السياق يقللان فرص تجاوز MFA.
- بعد أي اختراق، يجب مراجعة تغييرات الامتيازات، الحسابات الجديدة، وأجهزة MFA المسجلة، وتعطيل أي إضافات مشبوهة فوراً.
- مراقبة موافقات تطبيقات OAuth والحد من الأذونات عالية الحساسية مثل Mail.Read.All يقلل سطح الهجوم ويكشف محاولات الوصول الواسع للبيانات.

## المراجع

[1]: https://tryhackme.com/room/entraidmonitoring "TryHackMe — Entra ID Monitoring"
[2]: https://simontaplin.net/2026/08/02/answers-for-the-tryhackme-entra-id-monitoring-room/ "Answers for the TryHackMe Entra ID Monitoring Room — Simon Taplin"
[3]: https://tryhackme.com/room/entraidmonitoring/congratulations?step=records "Entra ID Monitoring — Final Completion Page"
