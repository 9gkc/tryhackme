# TryHackMe | Verified Write-ups

مستودع منظم لتوثيق غرف **TryHackMe** التي تم حلها والتحقق من إجاباتها داخل المختبر المصرح به. صُمم كل توثيق ليقود القارئ من فهم السيناريو إلى التحليل، ثم خطوات الحل، والإجابات النهائية، والدروس الأمنية، في **ملف Markdown واحد لكل غرفة**.

> **نطاق الاستخدام:** التدريب داخل مختبرات TryHackMe المصرح بها فقط.

## نظرة سريعة

| المؤشر | الحالة |
|---|---|
| الغرف الموثقة | **25 غرفة** |
| حالة الإجابات | **متحققة رسمياً داخل TryHackMe** |
| ملفات الغرف | **ملف واحد لكل غرفة** |
| التقييمات | لا يتم إرسالها ضمن سير العمل |
| حالة المستودع | **Private** |

## تنقل سريع

| القسم | الوصف |
|---|---|
| [الغرف المكتملة](#الغرف-المكتملة) | الفهرس الكامل مرتباً حسب تسلسل الإنجاز |
| [الغرف قيد التحقق](docs/unverified-rooms.md) | غرف لا تُدرج ضمن المكتملة حتى يثبت إكمالها |
| [منهجية الكتابة](docs/workflow.md) | القواعد المعتمدة لإضافة الغرف الجديدة |

## الغرف المكتملة

### 01–10 | SOC والدفاع والمراقبة

| # | الغرفة | المحور | التوثيق |
|---:|---|---|---|
| 01 | [Senior Security Analyst Intro](https://tryhackme.com/room/seniorsecanalystintro) | عقلية محلل SOC والتصعيد والتفكير الهجومي | [فتح الملف](rooms/01-senior-security-analyst-intro/README.md) |
| 02 | [SOC L2 Alert Triage](https://tryhackme.com/room/socl2alerttriage) | فرز التنبيهات، بناء الخط الزمني، والاحتواء | [فتح الملف](rooms/02-soc-l2-alert-triage/README.md) |
| 03 | [Report Writing for SOC L2](https://tryhackme.com/room/reportwritingsocl2) | كتابة الملخصات التنفيذية وتسليمات DFIR | [فتح الملف](rooms/03-report-writing-for-soc-l2/README.md) |
| 04 | [Defensive Security Trends](https://tryhackme.com/room/defensivesecuritytrends) | اتجاهات الدفاع الأمني وسلسلة التوريد والذكاء الاصطناعي | [فتح الملف](rooms/04-defensive-security-trends/README.md) |
| 05 | [Splunk: Exploring SPL](https://tryhackme.com/room/splunkexploringspl) | البحث في السجلات باستخدام SPL | [فتح الملف](rooms/05-splunk-exploring-spl/README.md) |
| 06 | [Monitoring Active Directory](https://tryhackme.com/room/monitoringactivedirectory) | مراقبة الهوية والمصادقة وتغييرات الصلاحيات | [فتح الملف](rooms/06-monitoring-active-directory/README.md) |
| 07 | [M365 Monitoring Basics](https://tryhackme.com/room/m365monitoringbasics) | مراقبة سجلات Microsoft 365 والهوية | [فتح الملف](rooms/07-m365-monitoring-basics/README.md) |
| 08 | [Entra ID Monitoring](https://tryhackme.com/room/entraidmonitoring) | مراقبة تسجيلات الدخول وسجلات Entra ID | [فتح الملف](rooms/08-entra-id-monitoring/README.md) |
| 09 | [Cloud Security Pitfalls](https://tryhackme.com/room/cloudsecuritypitfalls) | مخاطر حماية البيئات السحابية والهجرة | [فتح الملف](rooms/09-cloud-security-pitfalls/README.md) |
| 10 | [Threat Hunting: Introduction](https://tryhackme.com/room/threathuntingintroduction) | الصيد المبني على الفرضيات وتحسين الاكتشاف | [فتح الملف](rooms/10-threat-hunting-introduction/README.md) |

### 11–25 | استخبارات التهديدات، الويب، والاستجابة للحوادث

| # | الغرفة | المحور | التوثيق |
|---:|---|---|---|
| 11 | [Volt Typhoon](https://tryhackme.com/room/volttyphoon) | تحليل أساليب فاعل تهديد يستهدف البنية التحتية | [فتح الملف](rooms/11-volt-typhoon/README.md) |
| 12 | [Fools Mate, Revenge](https://tryhackme.com/room/foolsm8v2) | Prototype Pollution وتجاوز منطق تطبيق الشطرنج | [فتح الملف](rooms/12-fools-mate-revenge/README.md) |
| 13 | [ContAInment](https://tryhackme.com/room/containment) | تحليل PCAP والاستجابة لبرمجية الفدية | [فتح الملف](rooms/13-containment/README.md) |
| 14 | [Valenfind](https://tryhackme.com/room/lafb2026e10) | LFI، قراءة المصدر، واستخراج قاعدة البيانات | [فتح الملف](rooms/14-valenfind/README.md) |
| 15 | [Fools Mate](https://tryhackme.com/room/foolsmate) | تجاوز التحقق من جهة العميل والتلاعب بواجهة API | [فتح الملف](rooms/15-fools-mate/README.md) |
| 16 | [Corp Website](https://tryhackme.com/room/lafb2026e7) | React2Shell وRCE ثم التصعيد عبر sudo | [فتح الملف](rooms/16-corp-website/README.md) |
| 17 | [When Hearts Collide](https://tryhackme.com/room/lafb2026e1) | استغلال تصادمات MD5 في تطبيق ويب | [فتح الملف](rooms/17-when-hearts-collide/README.md) |
| 18 | [Signed Messages](https://tryhackme.com/room/lafb2026e8) | اشتقاق مفاتيح RSA القابلة للتنبؤ وتزوير التوقيع | [فتح الملف](rooms/18-signed-messages/README.md) |
| 19 | [TryHack3M: Bricks Heist](https://tryhackme.com/room/tryhack3mbricksheist) | WordPress RCE وتحليل عامل التعدين وربط المحفظة | [فتح الملف](rooms/19-bricks-heist/README.md) |
| 20 | [Extracted](https://tryhackme.com/room/extractedroom) | تحليل PCAP، تفريغ ذاكرة KeePass، واستعادة قاعدة بيانات مسروقة | [فتح الملف](rooms/20-extracted/README.md) |
| 21 | [Cache Me Outside](https://tryhackme.com/room/cachemeoutside) | OSINT وربط الهوية والبيانات العامة والقرائن الجغرافية | [فتح الملف](rooms/21-cache-me-outside/README.md) |
| 22 | [Digital Footprint](https://tryhackme.com/room/osintchallengeiv) | EXIF وWARC والبحث العكسي وبيانات المستندات | [فتح الملف](rooms/22-digital-footprint/README.md) |
| 23 | [CupidBot](https://tryhackme.com/room/lafb2026e6) | Web وprompt injection واستخراج أسرار وكيل AI | [فتح الملف](rooms/23-cupidbot/README.md) |
| 24 | [Water Bottle](https://tryhackme.com/room/waterbottle) | OSINT وتعقب محطة مياه تاريخية من قرائن الموقع والاتصال | [فتح الملف](rooms/24-water-bottle/README.md) |
| 25 | [Missing Person](https://tryhackme.com/room/missingperson) | OSINT وتحليل الصور وربط الفعالية بالمطعم والـDJ والكهف | [فتح الملف](rooms/25-missing-person/README.md) |

## بنية كل غرفة

```text
rooms/
└── NN-room-name/
    └── README.md
```

يجمع ملف الغرفة الواحد معلومات البيئة، ووصف الهدف، والتحليل، والخطوات العملية، والإجابات، والأعلام، ونتيجة التحقق الرسمي، والاستنتاجات الأمنية، والمراجع. لا توجد ملفات `solution.md` أو `notes.md` منفصلة.

## معيار الإكمال

لا تُدرج الغرفة في الفهرس إلا بعد قبول الإجابات داخل TryHackMe وظهور حالة الإكمال أو ما يثبت اكتمال المهمة رسمياً. لا يتم إرسال تقييم الغرفة، ولا تُعرض الغرف الجزئية على أنها مكتملة.

## إضافة الغرف القادمة

تُضاف كل غرفة جديدة برقم تسلسلي ومجلد مستقل وملف `README.md` واحد. يبدأ التوثيق بالهدف، ثم يشرح الملاحظة التي قادت إلى الخطوة التالية، وينتهي بالإجابات المتحققة والدروس الأمنية والمراجع المناسبة.

## الخصوصية

المستودع **Private**. لا تُضاف إليه بيانات الحسابات أو الرموز السرية أو المعلومات الشخصية. تُذكر عناوين IP المؤقتة فقط عندما تكون جزءاً من سياق المختبر، وتبقى جميع الخطوات ضمن نطاق TryHackMe المصرح به.
