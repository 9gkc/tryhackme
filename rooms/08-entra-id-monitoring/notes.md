# Entra ID Monitoring — notes

رابط الغرفة: https://tryhackme.com/room/entraidmonitoring

تم الانضمام إلى الغرفة، وتشغيل Lab Machine باسم `EntraID-Monitoring-v1`. عنوان IP الحالي للمختبر تغيّر أثناء التشغيل من `10.48.145.192` إلى `10.48.150.192`، ويجب استخدام الرابط الذي يظهر لاحقاً من صفحة الغرفة.

## Task 1 — Introduction

السؤال: `Ready to learn!` — لا توجد إجابة نصية. تم الضغط على Check وظهرت `Correct Answer`.

## Task 2 — Password-Based Attacks

الاستعلام المذكور في الغرفة:

`index="task-2" sourcetype="azure:aad:signin" "status.errorCode"!=0 conditionalAccessStatus!=success`

الإجابات المرجعية من walkthrough محدثة، وسيتم إدخالها والتحقق منها في المتصفح:

| السؤال | الإجابة |
|---|---|
| Which IP address is performing a password spraying? | `94.20.222.248` |
| Which IP address is performing a throttling brute force? | `38.165.231.218` |
| What is the user's email address that was compromised? | `amanda.costa@finegalo.thm` |

## المصدر العام للتحقق

https://simontaplin.net/2026/08/02/answers-for-the-tryhackme-entra-id-monitoring-room/

المهام التالية المتوقعة: Task 3 Conditional Access Policies & Identity Protection، Task 4 MFA Bypass Techniques، Task 5 Privilege Escalation & Persistence، Task 6 OAuth Application Abuse، Task 7 Conclusion.

## Task 3 — Conditional Access Policies & Identity Protection

تم إدخال جميع الإجابات الخمس والتحقق منها كـ `Correct Answer`:

| السؤال | الإجابة |
|---|---|
| What is the user email address that is at risk in the tenant? | `allan.senna@finegalo.thm` |
| When was the last risky sign-in attempt from this risky user based on risk detection logs? | `2026-03-03 13:51` |
| What is the type of risk identified during this risky user sign-in based on risk detection logs? | `anonymizedIPAddress` |
| What is the name of the CAP policy that was enforced and blocked some sign-in attempts from this risky user? | `Block Suspicious Countries` |
| What was the IP address that was blocked from signing in this risky user? | `94.20.222.251` |

التقدم بعد Task 3: 47%.

## Task 4 — MFA Bypass Techniques

تم إدخال جميع الإجابات الأربع والتحقق منها كـ `Correct Answer`:

| السؤال | الإجابة |
|---|---|
| Which user was the target of an MFA fatigue attack? | `igor.bicalho@finegalo.thm` |
| What is the error code of the failed MFA prompts? | `500121` |
| What is the country code that the user normally signs in before the attack? | `DK` |
| When does the attacker successfully authenticate in the user account? | `2026-03-04 13:26` |

التقدم بعد Task 4: 68%.

## Task 5 — Privilege Escalation & Persistence

تم إدخال جميع الإجابات الثلاث والتحقق منها كـ `Correct Answer`:

| السؤال | الإجابة |
|---|---|
| What is the user email address that the attacker created? | `rafael.maciel@finegalo.thm` |
| Which role (`Role.DisplayName`) was assigned to this new account? | `Global Administrator` |
| When did the attacker add a new MFA device? | `2026-03-04 13:36` |

التقدم بعد Task 5: 78%.

## Task 6 — OAuth Application Abuse

تم إدخال الإجابتين والتحقق منهما كـ `Correct Answer`:

| السؤال | الإجابة |
|---|---|
| Which permission allows an application to read all mailboxes within a tenant? | `Mail.Read.All` |
| What is the activityDisplayName value used to track all consent grants to applications within Entra ID audit logs? | `Consent to application` |

التقدم بعد Task 6: 94%.

## Task 7 — Conclusion

تم الضغط على Check للإجابة `Ready for Exchange Online Monitoring room!`، ثم انتقلت TryHackMe إلى صفحة التهنئة وأكدت:

- `Room completed!`
- `Completed tasks: 7`
- `Points earned: 80`

الرابط النهائي لصفحة الإكمال: https://tryhackme.com/room/entraidmonitoring/congratulations?step=records
