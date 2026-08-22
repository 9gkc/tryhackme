# TryHackMe — Monitoring Active Directory

رابط الغرفة: https://tryhackme.com/room/monitoringactivedirectory

تم إدخال جميع الإجابات والتحقق منها داخل المتصفح، وظهرت الحالة النهائية **Room completed: 100%**.

## الإجابات النهائية

| المهمة | السؤال المختصر | الإجابة |
|---|---|---|
| Task 1 | Introduction / تشغيل المختبر | لا توجد إجابة نصية؛ تم الضغط على Check |
| Task 2 | AD Traffic and Logging | لا توجد إجابة نصية؛ تم الضغط على Check |
| Task 3.1 | ملف تخزين بيانات اعتماد مستخدمي النطاق على Domain Controller | `NTDS.dit` |
| Task 3.2 | هل تسجل مصادقة المستخدم المحلي على Domain Controller؟ | `Nay` |
| Task 3.3 | Event ID لطلب TGT | `4768` |
| Task 3.4 | عدد الحسابات الفريدة التي طلبت TGT في `win` عبر كل الوقت | `14` |
| Task 4.1 | حقل اسم المجموعة في Splunk | `Group_Name` |
| Task 4.2 | أكثر Logon Type شيوعًا | `3` |
| Task 5.1 | لاحقة حسابات الكمبيوتر في Active Directory | `$` |
| Task 5.2 | أكثر خدمة مطلوبة في Event ID 4769 | `THM-DC$` |
| Task 6 | أمر عرض جميع إعدادات Audit Policy | `auditpol /get /category:*` |
| Task 7.1 | اسم الحساب المنشأ حديثًا | `nathan.brooks` |
| Task 7.2 | منشئ الحساب | `adm-luke.sullivan` |
| Task 7.3 | المجموعة التي أضيف إليها الحساب | `Marketing` |
| Task 7.4 | مصدر IP لأول طلب TGT للحساب `nathan.brooks` | `10.5.50.12` |
| Task 8 | Conclusion | لا توجد إجابة نصية؛ تم الضغط على Check |

## التحقق

ظهرت جميع الإجابات في الغرفة كـ **Correct Answer**، ووصلت نسبة التقدم إلى **100%**. كما تم تشغيل مختبر `monitoring-active-directory` بنجاح.

## المراجع

[1]: https://medium.com/@walidsalah231911/monitoring-active-directory-thm-5fcfbb0ba782 "Monitoring Active Directory — THM"

[2]: https://josepraveen.medium.com/monitoring-active-directory-tryhackme-splunk-5eca94d95250 "Monitoring Active Directory | TryHackMe | Splunk"
