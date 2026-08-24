# Missing Person — TryHackMe

> **الحالة:** اكتملت الغرفة رسمياً بعد قبول الإجابات الثماني. ظهرت الحالة `Room completed: 100%` وإشعار `5/9 Rooms completed!`. لم يتم اختيار درجة تقييم ولم يتم الضغط على **Submit now**.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط الرسمي | [TryHackMe — Missing Person][1] |
| التصنيف | OSINT / Image Investigation |
| الصعوبة | Easy |
| المدة | 30 دقيقة |
| عدد الأسئلة | 8 |
| بيئة التنفيذ | متصفح TryHackMe ومصادر عامة |

## الملخص التنفيذي

تحاكي الغرفة بلاغاً عن شخص اختفى بعد رحلة سياحية في عام 2025. تبدأ الأدلة بملفين مصورين، أحدهما لوجبة والآخر لفعالية MotoGP، ثم تتوسع إلى البحث الجغرافي، واستخراج البيانات الوصفية، وتحديد موقع حفلة، وربط DJ محلي بنشاط سياحي في كهف.[1] [2]

يقود تسلسل القرائن إلى جزيرة لومبوك في إندونيسيا: حلبة **Pertamina Mandalika International Street Circuit**، وفعالية أقيمت بين 3 و5 أكتوبر 2025، ومطعم **Cantina Mexicana**، ثم **Surfer’s Bar Kuta Lombok** وDJ باسم **Bong Leleh**. تكشف الحسابات العامة المرتبطة بالـDJ عن كهف **Gua Sumur** ورقم نشاط الجولات.

## مسار الحل

### 1. تحديد الحلبة وتاريخ الحدث

تظهر كلمة `PERTAMINA` في صورة MotoGP، وهي قرينة تقود إلى حلبة مانداليكا في لومبوك. يطابق البحث اسمها التجاري الكامل:

```text
Pertamina Mandalika International Street Circuit
```

وبالربط مع سباق MotoGP Indonesia لعام 2025، تكون فترة الحدث المطلوبة:

```text
03-05/10/2025
```

تتطابق هذه النتيجة مع صيغة التاريخ التي تطلبها المنصة `DD-DD/MM/YYYY`.[2] [3]

### 2. تحديد المطعم ووقت الصورة

يقود البحث العكسي عن صورة الطعام إلى **Cantina Mexicana** في Kuta Lombok. أما وقت الالتقاط فيُستخرج من البيانات الوصفية للصورة، حيث يظهر timestamp التالي:

```text
19:55:30
```

يوضح ذلك قيمة فحص EXIF في التحقيقات التي تحتوي على صور أصلية، مع ضرورة اعتبار البيانات الوصفية قرينة تحتاج إلى مقارنتها ببقية الأدلة.[2] [3]

### 3. تحديد موقع حفلة MotoGP

تذكر الرسالة الأخيرة حفلة بعد سباق MotoGP، ولا تشير إلى أن الحفلة أقيمت في المطعم نفسه. يقود البحث عن حفلة MotoGP في لومبوك إلى **Surfer’s Bar Kuta Lombok**. العنوان الذي قبلته المنصة حرفياً هو:

```text
Jl. Raya Kuta, Kuta, Kec. Pujut, Kabupaten Lombok Tengah, Nusa Tenggara Bar
```

> **ملاحظة تنسيقية:** استُخدمت كلمة `Bar` في نهاية العنوان لأنها الصيغة التي قبلها حقل الإجابة داخل TryHackMe.

### 4. تحديد الـDJ

بعد ربط الحفلة بالمنشورات العامة الخاصة بالفعالية، يظهر اسم الـDJ الذي لعب في تلك الليلة. الاسم المسرحي المقبول هو:

```text
Bong Leleh
```

ومن الأفضل في مثل هذا المسار فصل هوية المكان عن هوية الشخص؛ فالمطعم يمثل قرينة الرحلة، بينما منشورات الحفلة هي التي تقود إلى الـDJ.[2] [3]

### 5. تتبع النشاط السياحي

يقود البحث في الحسابات العامة المرتبطة باسم Bong Leleh إلى نشاط سياحي خاص بالكهوف. الكهف الذي يروّج الـDJ لزيارته هو:

```text
Gua Sumur
```

ويظهر رقم نشاط الجولات بالصيغة المحلية التي طلبها السؤال، أي من دون رمز الدولة:

```text
085333137345
```

## الإجابات النهائية

| # | السؤال | الإجابة المقبولة |
|---:|---|---|
| 1 | What is the commercial name of this circuit? | `Pertamina Mandalika International Street Circuit` |
| 2 | When did the event take place? | `03-05/10/2025` |
| 3 | What is the name of the restaurant? | `Cantina Mexicana` |
| 4 | At what time was this photo taken? | `19:55:30` |
| 5 | What is the full address of the bar’s location? | `Jl. Raya Kuta, Kuta, Kec. Pujut, Kabupaten Lombok Tengah, Nusa Tenggara Bar` |
| 6 | What is the DJ’s stage name? | `Bong Leleh` |
| 7 | What cave does he take tourists to? | `Gua Sumur` |
| 8 | What number did the DJ list for his tour business? | `085333137345` |

## التحقق الرسمي داخل TryHackMe

تم إدخال الإجابات الثماني في الحقول الرسمية، وظهرت عبارة **Correct Answer** لكل سؤال. بعد قبول الإجابة الأخيرة ظهرت حالة:

```text
Room completed: 100%
5/9 Rooms completed!
```

لم يتم إرسال تقييم الغرفة، ولم يتم اختيار أي درجة أو الضغط على **Submit now**.

## الدروس الأمنية

توضح الغرفة قوة الجمع بين الأدلة الضعيفة بدلاً من الاعتماد على نتيجة واحدة. فاسم ظاهر في صورة، وبيانات EXIF، وتاريخ فعالية، ومنشور حفلة، وحساب DJ، كلها تتحول إلى سلسلة تحقق متماسكة عند ربطها زمنياً وجغرافياً.

من منظور دفاعي، ينبغي تنظيف الصور من EXIF قبل مشاركتها، ومراجعة ما تكشفه منشورات الفعاليات عن الموقع والأشخاص، وفصل الحسابات الشخصية عن أنشطة الأعمال. وفي التحقيقات الواقعية يجب استخدام المعلومات العامة ضمن غرض قانوني محدد، وعدم التواصل مع الأشخاص أو اختبار أرقامهم دون تفويض.

## المراجع

[1]: https://tryhackme.com/room/missingperson "TryHackMe — Missing Person"
[2]: https://samuelmarques.dev/posts/missing-person/ "Write-up: Missing Person — Samuel M."
[3]: https://ivaylo-atanassov.com/blog/missing-person/ "Missing Person — Ivaylo Atanassov"
