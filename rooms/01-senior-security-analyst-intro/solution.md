# حل غرفة Senior Security Analyst Intro

تم إكمال غرفة TryHackMe **Senior Security Analyst Intro** بالكامل، وظهرت في صفحة الغرفة حالة **Room completed: 100%**.[1]

## الإجابات النهائية

| المهمة | السؤال أو المطلوب | الإجابة المقبولة |
|---|---|---|
| Task 1 — Journey to Senior | Let's get started! | لا تحتاج إلى إجابة؛ تم الضغط على Check |
| Task 2 — New Role, New Duties | Should you improve tech, soft, or both skills to become L2? | `Both` |
| Task 3 — Fun of Being SOC L2 | Does exploring new security areas help you grow? (Yea/Nay) | `Yea` |
| Task 4 — L1 vs L2 Mindset Shift | What mindset helps you see and predict how incidents unfold? | `Attacker Mindset` |
| Task 5 — Your Day as Level 2 | What flag did you get after completing the challenge? | `THM{much_more_than_alert_triage}` |
| Task 6 — Next Steps | Complete the room! | لا تحتاج إلى إجابة؛ تم الضغط على Check |

## ملخص التحدي العملي

في **SIEM Search**، بُني التسلسل الزمني للحادثة على الجهاز `LPT-0152`. بدأ النشاط بتنزيل `ReleaseNotes.pdf.exe` من Microsoft Edge، ثم تشغيل `loader.exe`، ثم تحميل `beacon.dll` عبر `rundll32.exe`. كانت الاستجابة الصحيحة هي عزل الجهاز، إكمال التحليل، وتنظيف المضيف من البرمجية الخبيثة.

في **SIEM Rules**، عولجت مشكلة عدم كشف الملفات ذات الامتداد المزدوج بإضافة قاعدة للتنزيلات مثل `*.pdf.exe` و`*.pdf.lnk`. وبعد ظهور النتائج الإيجابية الكاذبة من مجلد `C:\Program Files\TryHackMeToolkit\`، تم تطبيق استثناء للمجلد بالتنسيق مع فريق IT، ثم اختيار الإجراء `Quarantine the file` واختبار القاعدة بنجاح.

في **Threat Reports**، تمت مراجعة تقرير Akira RaaS المتعلق باستغلال Sonicwall SSL-VPN. الإجراء الصحيح كان شرح المخاطر العالية لفريق IT ومساعدته في التخفيف، ثم تلخيص التقرير ومشاركة المؤشرات والتنبيه في دردشة SOC.

## الحالة النهائية

أُرسلت جميع الإجابات بنجاح، وارتفع تقدم الغرفة إلى **100%**. العلم الذي ظهر في التطبيق وأُدخل في الغرفة هو:

> `THM{much_more_than_alert_triage}`

## المراجع

[1]: https://tryhackme.com/room/seniorsecanalystintro — صفحة غرفة TryHackMe: Senior Security Analyst Intro.
[2]: https://static-labs.tryhackme.cloud/apps/senior-security-analyst-intro/ — التطبيق التدريبي المضمّن المستخدم لإكمال Task 5.
