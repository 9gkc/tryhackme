# TryHackMe — Verified Room Write-ups

هذا المستودع يوثق غرف TryHackMe التي تم حلها داخل المتصفح المصرح به، مع الحفاظ على تسلسل واضح بين فهم السيناريو، والتحليل، والخطوات العملية، والإجابة النهائية، ثم دليل التحقق الرسمي داخل المنصة. جميع المحتويات مخصصة للتدريب داخل مختبرات TryHackMe المصرح بها فقط.

## الفهرس

| # | الغرفة | المجال | الحالة | الملف الوحيد |
|---|---|---|---|---|
| 01 | [Senior Security Analyst Intro](https://tryhackme.com/room/seniorsecanalystintro) | SOC analyst mindset, escalation, and attacker thinking. | **Officially completed** | [Write-up](rooms/01-senior-security-analyst-intro/README.md) |
| 02 | [SOC L2 Alert Triage](https://tryhackme.com/room/socl2alerttriage) | L2 alert triage, timelines, containment, and escalation. | **Officially completed** | [Write-up](rooms/02-soc-l2-alert-triage/README.md) |
| 03 | [Report Writing for SOC L2](https://tryhackme.com/room/reportwritingsocl2) | Executive summaries, DFIR handovers, and responsible AI use. | **Officially completed** | [Write-up](rooms/03-report-writing-for-soc-l2/README.md) |
| 04 | [Defensive Security Trends](https://tryhackme.com/room/defensivesecuritytrends) | Modern defensive security practices and evolving defender capabilities. | **Officially completed** | [Write-up](rooms/04-defensive-security-trends/README.md) |
| 05 | [Splunk: Exploring SPL](https://tryhackme.com/room/splunkexploringspl) | Search Processing Language, filtering, fields, and aggregation. | **Officially completed** | [Write-up](rooms/05-splunk-exploring-spl/README.md) |
| 06 | [Monitoring Active Directory](https://tryhackme.com/room/monitoringactivedirectory) | Identity monitoring, authentication anomalies, and privilege changes. | **Officially completed** | [Write-up](rooms/06-monitoring-active-directory/README.md) |
| 07 | [M365 Monitoring Basics](https://tryhackme.com/room/m365monitoringbasics) | Microsoft 365 audit activity, identity events, and SIEM monitoring. | **Officially completed** | [Write-up](rooms/07-m365-monitoring-basics/README.md) |
| 08 | [Entra ID Monitoring](https://tryhackme.com/room/entraidmonitoring) | Entra ID sign-ins, audit logs, privilege changes, and identity detections. | **Officially completed** | [Write-up](rooms/08-entra-id-monitoring/README.md) |
| 09 | [Cloud Security Pitfalls](https://tryhackme.com/room/cloudsecuritypitfalls) | Cloud workload protection, runtime visibility, and migration risks. | **Officially completed** | [Write-up](rooms/09-cloud-security-pitfalls/README.md) |
| 10 | [Threat Hunting: Introduction](https://tryhackme.com/room/threathuntingintroduction) | Hypothesis-driven hunting, telemetry, behavior testing, and detection improvement. | **Officially completed** | [Write-up](rooms/10-threat-hunting-introduction/README.md) |
| 11 | [Volt Typhoon](https://tryhackme.com/room/volttyphoon) | Threat actor tradecraft and stealthy critical-infrastructure intrusion activity. | **Officially completed** | [Write-up](rooms/11-volt-typhoon/README.md) |
| 12 | [Fools Mate, Revenge](https://tryhackme.com/room/foolsm8v2) | Prototype pollution in a chess application and server-side state abuse. | **Officially completed** | [Write-up](rooms/12-fools-mate-revenge/README.md) |
| 13 | [ContAInment](https://tryhackme.com/room/containment) | Ransomware response, PCAP investigation, recovery, and evidence validation. | **Officially completed** | [Write-up](rooms/13-containment/README.md) |
| 14 | [Valenfind](https://tryhackme.com/room/lafb2026e10) | Local file inclusion, source discovery, secrets, and database extraction. | **Officially completed** | [Write-up](rooms/14-valenfind/README.md) |
| 15 | [Fools Mate](https://tryhackme.com/room/foolsmate) | Client-side validation bypass and direct manipulation of a backend move API. | **Officially completed** | [Write-up](rooms/15-fools-mate/README.md) |
| 16 | [Corp Website](https://tryhackme.com/room/lafb2026e7) | React2Shell RCE, command execution as daniel, and sudo-based privilege escalation. | **Officially completed** | [Write-up](rooms/16-corp-website/README.md) |
| 17 | [When Hearts Collide](https://tryhackme.com/room/lafb2026e1) | MD5 collision abuse in a web application that matches uploaded images to dogs. | **Officially completed** | [Write-up](rooms/17-when-hearts-collide/README.md) |
| 18 | [Signed Messages](https://tryhackme.com/room/lafb2026e8) | Predictable RSA key derivation, signature forgery, and trust-model failure. | **Officially completed** | [Write-up](rooms/18-signed-messages/README.md) |
| 19 | [TryHack3M: Bricks Heist](https://tryhackme.com/room/tryhack3mbricksheist) | WordPress RCE, miner persistence, wallet attribution, and incident analysis. | **Officially completed** | [Write-up](rooms/19-bricks-heist/README.md) |

## منهجية التوثيق

كل غرفة موجودة داخل مجلد مستقل مرقّم للحفاظ على ترتيب الإنجاز وسهولة القراءة. يبدأ ملف `README.md` واحداً يجمع الملخص والحل المتسلسل والأجوبة والأدلة والدروس والمراجع. لا تُضاف الغرفة إلى الفهرس إلا بعد ظهور الإجابة الصحيحة أو حالة الإكمال الرسمية داخل TryHackMe وفق ما تم توثيقه.

## سير العمل للغرف القادمة

عند حل غرفة جديدة، تُضاف بعد التحقق الرسمي إلى مجلد مستقل يحتوي ملف `README.md` واحداً يجمع معلومات الغرفة، الهدف، التحليل، خطوات الحل، الإجابات، دليل التحقق، الدروس الأمنية، والمراجع. الغرف التي لم يثبت إكمالها رسمياً تبقى خارج الفهرس إلى أن تكتمل.

## ملاحظة الخصوصية

المستودع منشأ كـ **Private repository**. لا تُضاف إليه بيانات الحسابات أو الرموز السرية أو معلومات خارج نطاق المختبر، وتُستخدم عناوين IP المؤقتة فقط عندما تكون جزءاً من شرح المختبر.
