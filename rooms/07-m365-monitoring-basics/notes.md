# M365 Monitoring Basics — notes

رابط الغرفة: https://tryhackme.com/room/m365monitoringbasics

تم الانضمام إلى الغرفة. Task 1 سؤال معلوماتي فقط: `Let's start!` ثم Check، وقد تم التحقق منه.

## الإجابات المؤكدة

| السؤال | الإجابة | الحالة |
|---|---|---|
| Task 2.1 What type of application is Entra ID? | Identity Provider | Correct Answer |
| Task 2.2 What type of identity is a server account? | Device | Correct Answer |
| Task 3.1 What authentication resource can prevent attackers from authenticating with only a stolen password? | MFA | Correct Answer |
| Task 3.2 What can help us detect and monitor cloud identity threats? | Logs | Correct Answer |

## Task 4 — Entra ID Sign-in Logs

تم تشغيل Lab Machine بعنوان IP `10.48.145.118`، وظهر رابط Splunk reverse proxy:

`https://10-48-145-118.reverse-proxy.cell-prod-ap-south-1a.vm.tryhackme.com`

تم إدخال الإجابات الخمس والتحقق منها كـ Correct Answer:

| السؤال | الإجابة |
|---|---|
| What is the email address of the compromised identity? | allan.smith@finegalo.thm |
| What is the IP address used by the attacker? | 2804:2488:7082:a4c0:fd97:b11b:9895:49c0 |
| What is the city of the IP address used by the attacker? | Belo Horizonte |
| When was the first successful sign-in? | 2/11/26 6:16:53.000 PM |
| What is the first application after the Office home page? | One Outlook Web |

ملاحظات التحقيق: 25 فشلاً برمز 50126، ثم نجاحات؛ الحقول المهمة userPrincipalName وipAddress وappDisplayName وlocation.city وstatus.errorCode.

## Task 5 — Entra ID Audit Logs

الاستعلام الأساسي: `index=scenario sourcetype="azure:aad:audit"`، والحقول المهمة activityDisplayName وinitiatedBy وtargetResources. تم التحقق من الإجابات الثلاث:

| السؤال | الإجابة |
|---|---|
| What was the first change made by the attacker in the compromised user account? | User started security info registration |
| What is the activityDisplayName that reveals all the details of the modified properties in a user? | Update user |
| What is the second change made in the account? | Reset password (self-service) |

## Task 6 — M365 Introduction

تمت قراءة المقدمة والضغط على Check، وظهرت Correct Answer. تشرح المهمة خدمات Exchange Online وSharePoint وOneDrive وTeams وسجلات Unified Audit Log.

## Task 7 — M365 Audit Logs

الاستعلام الأساسي: `index="scenario" sourcetype="o365:management:activity"`. تم إدخال الإجابات الخمس والتحقق منها كـ Correct Answer:

| السؤال | الإجابة |
|---|---|
| What is the application used by the attacker? | Exchange |
| What is the change made in the user application by the attacker? | New-InboxRule |
| What is the subject of the email message sent by the attacker? | URGENT: Approval for new internal VPN Access |
| When did the attacker access the response to the message? | 2/11/26 6:20:09.000 PM |
| Which path was the response stored in? | \\Deleted Items |

التقدم الحالي في الغرفة: 95%. المتبقي هو فتح Task 8 والضغط على Check ثم التحقق من إكمال الغرفة.

## المصادر الخارجية للتحقق

- https://classroom.anir0y.in/post/thm-room-m365monitoringbasics/
- https://simontaplin.net/2026/06/14/answers-for-the-tryhackme-m365-monitoring-basics-room/
