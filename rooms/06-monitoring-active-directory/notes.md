# Monitoring Active Directory — notes

المختبر قيد التشغيل في TryHackMe، وسيتم إدخال الإجابات في المتصفح والتحقق منها.

## الإجابات المؤكدة من شرح الغرفة ومرجعين محدثين

Task 1: لا توجد إجابة نصية؛ تشغيل المختبر ثم Check.
Task 2: لا توجد إجابة نصية؛ قراءة AD Traffic and Logging ثم Check.

Task 3 Authentication Events:
- ملف بيانات اعتماد مستخدمي النطاق على DC: `NTDS.dit`
- مصادقة المستخدم المحلي على workstation تولد أحداثًا على DC؟ `Nay`
- Event ID لطلب TGT: `4768`
- عدد الحسابات الفريدة التي طلبت TGT في win عبر كل الوقت: `14`

Task 4 Accounts, Groups and Resource Access Events:
- الحقل الذي يحتوي اسم المجموعة: `Group_Name`
- أكثر Logon Type شيوعًا: `3`

Task 5 Understanding Baseline Activity:
- لاحقة حسابات الكمبيوتر: `$`
- الخدمة الأكثر طلبًا: `THM-DC$`

Task 6 Audit Policy Configuration:
- `auditpol /get /category:*`

Task 7 Scenario — New Employee Onboarding Audit:
- الحساب المنشأ: `nathan.brooks`
- منشئ الحساب: `adm-luke.sullivan`
- المجموعة: `Marketing`
- مصدر IP لأول TGT: `10.5.50.12`

المراجع العامة المقروءة:
- https://medium.com/@walidsalah231911/monitoring-active-directory-thm-5fcfbb0ba782
- https://josepraveen.medium.com/monitoring-active-directory-tryhackme-splunk-5eca94d95250

تم التحقق في المتصفح من إكمال Task 3 وTask 4 بنسبة تقدم 50%. إجابات Task 4 الظاهرة كـ Correct Answer هي `Group_Name` و`3`. Task 5 مفتوح، وتظهر أسئلته عن لاحقة حسابات الكمبيوتر والخدمة الأكثر طلبًا؛ الإجابتان المتوقعـتان `$` و`THM-DC$`.
