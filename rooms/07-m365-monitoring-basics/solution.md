# TryHackMe — M365 Monitoring Basics

**رابط الغرفة:** https://tryhackme.com/room/m365monitoringbasics  
**النتيجة:** **Room completed: 100%**  
**المختبر المستخدم:** Intro-EntraID-M365-Splunk-v3  
**عنوان المختبر أثناء الحل:** `10.48.145.118`  
**حالة الإجابات:** تم إدخال جميع الإجابات والتحقق منها داخل متصفح TryHackMe وظهرت `Correct Answer`.

## ملخص التحقيق

توضح الغرفة سلسلة اختراق هوية سحابية بدأت بمحاولات فاشلة متكررة لتسجيل الدخول، تلتها مصادقة ناجحة من عنوان IP في Belo Horizonte. بعد ذلك انتقل المهاجم إلى Outlook، سجّل معلومات أمان، حدّث الحساب وأعاد تعيين كلمة المرور، ثم أنشأ قاعدة واردة وأرسل رسالة تصيّد داخلية وقرأ الرد من مجلد العناصر المحذوفة.

## الإجابات

| المهمة | السؤال | الإجابة |
|---|---|---|
| Task 1 | Let's start! | لا توجد إجابة نصية؛ تم الضغط على Check |
| Task 2 | What type of application is Entra ID? | `Identity Provider` |
| Task 2 | What type of identity is a server account? | `Device` |
| Task 3 | What authentication resource can prevent attackers from authenticating with only a stolen password? | `MFA` |
| Task 3 | What can help us detect and monitor cloud identity threats? | `Logs` |
| Task 4 | What is the email address of the compromised identity? | `allan.smith@finegalo.thm` |
| Task 4 | What is the IP address used by the attacker? | `2804:2488:7082:a4c0:fd97:b11b:9895:49c0` |
| Task 4 | What is the city of the IP address used by the attacker? | `Belo Horizonte` |
| Task 4 | When was the first successful sign-in in the compromised account after the failure attempts? | `2/11/26 6:16:53.000 PM` |
| Task 4 | What is the first application the attacker accessed after the office home page? | `One Outlook Web` |
| Task 5 | What was the first change made by the attacker in the compromised user account? | `User started security info registration` |
| Task 5 | What is the activityDisplayName that reveals all the details of the modified properties in a user? | `Update user` |
| Task 5 | What is the second change made in the account? | `Reset password (self-service)` |
| Task 6 | Let's explore M365 logs! | لا توجد إجابة نصية؛ تم الضغط على Check |
| Task 7 | What is the application used by the attacker? | `Exchange` |
| Task 7 | What is the change made in the user application by the attacker? | `New-InboxRule` |
| Task 7 | What is the subject of the email message sent by the attacker? | `URGENT: Approval for new internal VPN Access` |
| Task 7 | When did the attacker access the response to the message? | `2/11/26 6:20:09.000 PM` |
| Task 7 | Which path was the response stored in? | `\Deleted Items` |
| Task 8 | Ready to explore Entra ID threats! | لا توجد إجابة نصية؛ تم الضغط على Check |

## تسلسل الأحداث المستنتج من السجلات

| المرحلة | الدليل |
|---|---|
| اكتشاف الهوية المخترقة | حساب `allan.smith@finegalo.thm`، وعنوان المهاجم `2804:2488:7082:a4c0:fd97:b11b:9895:49c0` من مدينة Belo Horizonte |
| بداية الدخول الناجح | `2/11/26 6:16:53.000 PM` بعد محاولات فاشلة برمز 50126 |
| الوصول إلى البريد | التطبيق الأول بعد `OfficeHome` هو `One Outlook Web` |
| تثبيت الاستمرارية على مستوى الهوية | `User started security info registration` ثم `Update user` ثم `Reset password (self-service)` |
| تثبيت الاستمرارية في البريد | إنشاء قاعدة `New-InboxRule` في خدمة `Exchange` |
| التصيّد الداخلي | إرسال رسالة بعنوان `URGENT: Approval for new internal VPN Access` |
| إخفاء وقراءة الرد | تمت قراءة الرد في `2/11/26 6:20:09.000 PM` من `\Deleted Items` |

## ملاحظات تقنية

الاستعلامات الأساسية المستخدمة في المختبر كانت:

```text
index=scenario sourcetype="azure:aad:signin"
index=scenario sourcetype="azure:aad:audit"
index="scenario" sourcetype="o365:management:activity"
```

ينبغي استخدام نطاق الزمن **All Time** في Splunk لأن بيانات السيناريو مؤرخة في فبراير 2026.

## مصادر التحقق العامة

- [TryHackMe — M365 Monitoring Basics](https://tryhackme.com/room/m365monitoringbasics)
- [Walkthrough — Classroom](https://classroom.anir0y.in/post/thm-room-m365monitoringbasics/)
- [Answers — Simon Taplin](https://simontaplin.net/2026/06/14/answers-for-the-tryhackme-m365-monitoring-basics-room/)
