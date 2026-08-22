# M365 Monitoring Basics — TryHackMe

> **الحالة:** Room completed: 100% — تم إدخال جميع الإجابات والتحقق منها داخل متصفح TryHackMe وظهرت "Correct Answer". لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط | https://tryhackme.com/room/m365monitoringbasics |
| التصنيف/المجال | — |
| الصعوبة | — |
| المختبر المستخدم | Intro-EntraID-M365-Splunk-v3 |
| عنوان المختبر أثناء الحل | 10.48.145.118 |

## الملخص التنفيذي

يغطي هذا المختبر أساسيات مراقبة هويات M365 عبر Entra ID وM365 Audit Logs باستخدام Splunk. يتتبع السيناريو سلسلة اختراق لهوية سحابية بدأت بمحاولات فاشلة متكررة لتسجيل الدخول (رمز الخطأ 50126)، تلاها تسجيل دخول ناجح من عنوان IPv6 مصدره مدينة Belo Horizonte. بعد المصادقة، انتقل المهاجم إلى One Outlook Web، وبدأ تسجيل معلومات الأمان، ثم حدّث خصائص الحساب وأعاد تعيين كلمة المرور. لاحقاً، ثبّت استمرارية داخل البريد عبر إنشاء قاعدة وارد جديدة، وأرسل رسالة تصيّد داخلي بعنوان محدد، ثم قرأ الرد لاحقاً من مجلد Deleted Items. [1]

## مسار الحل

### 1. Entra ID Sign-in Logs (Task 4)

- الوصول إلى Splunk عبر reverse proxy الخاص بالمختبر.
- استخدام نطاق الزمن All Time نظراً لأن بيانات السيناريو تعود إلى فبراير 2026.
- الاستعلام الأساسي:
  ```text
  index=scenario sourcetype="azure:aad:signin"
  ```
- الحقول المفحوصة: userPrincipalName وipAddress وappDisplayName وlocation.city وstatus.errorCode.
- النتائج:
  - الهوية المخترقة: allan.smith@finegalo.thm.
  - عنوان IP للمهاجم: 2804:2488:7082:a4c0:fd97:b11b:9895:49c0، المدينة: Belo Horizonte.
  - أول تسجيل دخول ناجح بعد إخفاقات متتالية (50126): 2/11/26 6:16:53.000 PM.
  - أول تطبيق بعد OfficeHome: One Outlook Web.

### 2. Entra ID Audit Logs (Task 5)

- الاستعلام الأساسي:
  ```text
  index=scenario sourcetype="azure:aad:audit"
  ```
- الحقول المفحوصة: activityDisplayName وinitiatedBy وtargetResources.
- التسلسل الزمني لتغييرات الهوية:
  - User started security info registration.
  - Update user (يكشف تفاصيل الخصائص المعدّلة).
  - Reset password (self-service).

### 3. M365 Audit Logs (Task 7)

- الاستعلام الأساسي:
  ```text
  index="scenario" sourcetype="o365:management:activity"
  ```
- النتائج على مستوى تطبيق Exchange:
  - التطبيق المستخدم: Exchange.
  - التغيير المجراة: New-InboxRule.
  - عنوان رسالة التصيّد المرسلة: URGENT: Approval for new internal VPN Access.
  - زمن الوصول إلى الرد: 2/11/26 6:20:09.000 PM.
  - مسار حفظ الرد: \Deleted Items.

## الإجابات النهائية

| المهمة | السؤال | الإجابة المقبولة |
|---|---|---|
| Task 1 | Let's start! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| Task 2 | What type of application is Entra ID? | Identity Provider |
| Task 2 | What type of identity is a server account? | Device |
| Task 3 | What authentication resource can prevent attackers from authenticating with only a stolen password? | MFA |
| Task 3 | What can help us detect and monitor cloud identity threats? | Logs |
| Task 4 | What is the email address of the compromised identity? | allan.smith@finegalo.thm |
| Task 4 | What is the IP address used by the attacker? | 2804:2488:7082:a4c0:fd97:b11b:9895:49c0 |
| Task 4 | What is the city of the IP address used by the attacker? | Belo Horizonte |
| Task 4 | When was the first successful sign-in in the compromised account after the failure attempts? | 2/11/26 6:16:53.000 PM |
| Task 4 | What is the first application the attacker accessed after the office home page? | One Outlook Web |
| Task 5 | What was the first change made by the attacker in the compromised user account? | User started security info registration |
| Task 5 | What is the activityDisplayName that reveals all the details of the modified properties in a user? | Update user |
| Task 5 | What is the second change made in the account? | Reset password (self-service) |
| Task 6 | Let's explore M365 logs! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| Task 7 | What is the application used by the attacker? | Exchange |
| Task 7 | What is the change made in the user application by the attacker? | New-InboxRule |
| Task 7 | What is the subject of the email message sent by the attacker? | URGENT: Approval for new internal VPN Access |
| Task 7 | When did the attacker access the response to the message? | 2/11/26 6:20:09.000 PM |
| Task 7 | Which path was the response stored in? | \Deleted Items |
| Task 8 | Ready to explore Entra ID threats! | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |

## التحقق الرسمي داخل TryHackMe

- ظهرت حالة Room completed: 100%.
- عند إدخال كل إجابة والضغط على Check، عُرضت عبارة Correct Answer داخل واجهة TryHackMe.
- للمهام التي لا تتطلب إدخال نصي (Task 1 وTask 6 وTask 8)، تم الضغط على Check فقط وتأكد القبول.
- لا يوجد ذكر في المسودة بشأن إرسال تقييم.

## الدروس الأمنية

- تفعيل MFA يقلل خطر الاستغلال المبني على كلمات مرور مسروقة، كما أن مراجعة سجلات Entra ID وM365 بانتظام تكشف الأنماط الشاذة مثل تغيير معلومات الأمان وعمليات Reset password.
- إنشاء Inbox rules الخبيثة مؤشر شائع على تثبيت استمرارية داخل البريد؛ يجب مراقبة أحداث New-InboxRule والتنبيهات على الرسائل المشبوهة.
- استخدام أدوات البحث مثل Splunk مع نطاق زمني مناسب (All Time لبيانات مؤرشفة) يضمن عدم فقدان أدلة زمنية حرجة.
- مؤشرات الجغرافيا وعناوين IP (مثل مدينة Belo Horizonte وعنوان IPv6 المستخدَم) تساعد في التحليل السياقي لوقائع المصادقة.

## المراجع

[1]: https://tryhackme.com/room/m365monitoringbasics
[2]: https://classroom.anir0y.in/post/thm-room-m365monitoringbasics/
[3]: https://simontaplin.net/2026/06/14/answers-for-the-tryhackme-m365-monitoring-basics-room/
