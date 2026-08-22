# Splunk: Exploring SPL — TryHackMe

> **الحالة:** تم إكمال الغرفة بنجاح. ظهرت جميع الإجابات كـ "Correct Answer" ضمن TryHackMe، كما ظهر مؤشر "Room completed: 100%" في الواجهة. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط | [TryHackMe: Splunk: Exploring SPL][1] |
| التصنيف/المجال | غير مذكور في المسودة |
| الصعوبة | غير مذكور في المسودة |
| المدة/المختبر | Lab Machine: Exploring SPL v5 |

## الملخص التنفيذي

تهدف غرفة Splunk: Exploring SPL إلى تدريب المستخدم على أساسيات SPL في Splunk عبر سلسلة من المهام العملية: البحث وتجميع النتائج، استخدام عوامل البحث، التصفية بالـ regex، هيكلة النتائج بأوامر مثل table وreverse، وتحويلها بأوامر مثل iplocation والـ lookup، ثم ملاحظة أنماط الشذوذ. تم تنفيذ الاستعلامات داخل واجهة Splunk الخاصة بالمختبر والتحقق من القيم المطلوبة لكل سؤال ضمن TryHackMe.

اعتمد التحقق على نتائج الواجهة المباشرة، بما في ذلك مثال Task 2 الذي أكد أن الاستعلام index=windowslogs عبر All time يُظهر 12,256 حدثاً، مع استكمال بقية الاستعلامات للوصول إلى القيم النهائية.

## مسار الحل

### 1. تهيئة المختبر والوصول إلى Splunk

- تم تشغيل المختبر والولوج إلى واجهة Splunk عبر رابط المختبر: https://LAB_WEB_URL.p.thmlabs.com.
- جرى استخدام محدد الزمن All time عند الحاجة لضمان شمول كل الأحداث.

### 2. Task 2 — Search & Reporting

- تنفيذ الاستعلام:
  ```
  index=windowslogs
  ```
  مع All time أعاد 12,256 حدثاً.
- تحليل الحقول أظهر أعلى SourceIP من حيث عدد الأحداث.
- باستخدام مُحدد الزمن لليوم 04/15/2022 بين 08:05 AM و08:06 AM تم الحصول على عدد الأحداث ضمن هذه الدقيقة.

النتائج المقبولة:
- إجمالي الأحداث: 12256.
- أعلى SourceIP: 172.90.12.11.
- عدد أحداث 04/15/2022 من 08:05 إلى 08:06: 134.

### 3. Task 3 — Search Operators

- تصفية أحداث EventID:
  ```
  index=windowslogs EventID=4624
  ```
  وإحصاء النتائج: 26.
- دمج شروط الوجهة:
  ```
  index=windowslogs DestinationIp=172.18.39.6 DestinationPort=135
  ```
  وإحصاء النتائج: 4.
- استعلام مُقيّد بالمضيف والوجهة:
  ```
  index=windowslogs Hostname=Salena.Adam DestinationIp=172.18.38.5
  ```
  ثم إحصاء أعلى SourceIp: 172.90.12.11.
- البحث بالتوسّع باستخدام wildcards:
  ```
  cyber*
  ```
  وأعاد 12256.
- أولوية عوامل البحث: الأدنى هي AND.

### 4. Task 4 — Filtering Results

- تحديد أعلى قيمة لـ SourceProcessId عبر تجميع النتائج: 9496.
- استخدام regex لتصفية TargetObject المنتهي بـ "Manager":
  ```
  ... | regex TargetObject="Manager$"
  ```
  وأعلى TargetObject: HKLM\\SOFTWARE\\Microsoft\\SecurityManager.

### 5. Task 5 — Structuring Results

- استخدام table لاستعراض الحقول، فظهر أول AccountName: SYSTEM.
- عكس ترتيب النتائج باستخدام:
  ```
  ... | reverse
  ```
  فكان أول EventID بعد العكس: 800.
- العثور على بيانات اعتماد A1berto كما ظهرت في النتائج: كلمة المرور paw0rd1.

### 6. Task 6 — Transforming Commands

- تحديد أكثر قيمة تكراراً في Image: C:\windows\system32\svchost.exe.
- تطبيق iplocation على عناوين IP للحصول على Region: California.
- استخدام lookup RiskScore وربطه بالحقل Image؛ أعلى Image: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe.

### 7. Task 7 — Anomaly Detection

- ملاحظة مستخدم خارج النمط: jsmith.
- الدولة الشاذة لهذا المستخدم: JP.
- المستخدم الذي سجّل دخولاً عند الثالثة صباحاً: njackson.

## الإجابات النهائية

| المهمة/السؤال | الإجابة المقبولة |
|---|---|
| Task 1 — Introduction / تشغيل المختبر | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| Task 2.1 — إجمالي أحداث index=windowslogs | `12256` |
| Task 2.2 — أعلى SourceIP من حيث الأحداث | `172.90.12.11` |
| Task 2.3 — أحداث 04/15/2022 من 08:05 إلى 08:06 | `134` |
| Task 3.1 — عدد أحداث EventID=4624 | `26` |
| Task 3.2 — DestinationIp=172.18.39.6 وDestinationPort=135 | `4` |
| Task 3.3 — أعلى SourceIp لاستعلام Hostname=Salena.Adam | `172.90.12.11` |
| Task 3.4 — نتائج البحث عن cyber* | `12256` |
| Task 3.5 — العامل ذو الأولوية الأدنى | `AND` |
| Task 4.1 — أعلى SourceProcessId | `9496` |
| Task 4.2 — أعلى TargetObject مع regex "Manager$" | `HKLM\\SOFTWARE\\Microsoft\\SecurityManager` |
| Task 5.1 — أول AccountName في table | `SYSTEM` |
| Task 5.2 — أول EventID بعد reverse | `800` |
| Task 5.3 — كلمة مرور المستخدم A1berto | `paw0rd1` |
| Task 6.1 — أكثر قيمة تكرارًا في Image | `C:\\windows\\system32\\svchost.exe` |
| Task 6.2 — Region بعد iplocation | `California` |
| Task 6.3 — أعلى Image في lookup RiskScore | `C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe` |
| Task 7.1 — المستخدم الخارج عن النمط | `jsmith` |
| Task 7.2 — الدولة الشاذة للمستخدم السابق | `JP` |
| Task 7.3 — المستخدم الذي سجّل دخولًا عند 03:00 | `njackson` |
| Task 8 — Conclusion | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |

## التحقق الرسمي داخل TryHackMe

- ضمن واجهة TryHackMe ظهرت مؤشرات "Correct Answer" لجميع أسئلة Tasks 2–7، كما ظهر "Correct Answer" لـ Task 8.
- الحالة النهائية للغرفة عُرضت بوضوح: "Room completed: 100%".
- لم يُرسل تقييم الغرفة.

## الدروس الأمنية

- صياغة استعلامات SPL بدقة، واستخدام عوامل البحث والأولوية المنطقية، ضرورية للوصول إلى نتائج موثوقة.
- الجمع بين أوامر الهيكلة والتحويل مثل table وreverse وiplocation والـ lookup يثري التحليل ويُبرز الشذوذ سلوكياً وجغرافياً.
- ضبط النطاق الزمني بدقة يؤثر مباشرةً على العدّ والإحصاءات، وهو خطوة محورية قبل تفسير النتائج.

## المراجع

[1]: https://tryhackme.com/room/splunkexploringspl
[2]: https://simontaplin.net/2026/07/25/answers-for-the-tryhackme-splunk-exploring-spl-room/
