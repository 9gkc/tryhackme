# Digital Footprint — TryHackMe

> **الحالة:** اكتملت الغرفة رسمياً بعد قبول الإجابات الأربع. ظهرت صفحة الإكمال برسالة `Room completed!` مع `Completed tasks: 4` و`Points earned: 120`. لم يتم اختيار درجة تقييم ولم يتم الضغط على **Submit now**.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط الرسمي | [TryHackMe — Digital Footprint][1] |
| الاسم في الرابط | OSINT Challenge IV |
| التصنيف | OSINT / Digital Footprint |
| الصعوبة | Easy |
| المدة | 60 دقيقة |
| عدد المهام | 4 |
| بيئة التنفيذ | AttackBox داخل TryHackMe |

## الملخص التنفيذي

تختبر الغرفة مهارات التحقيق في المصادر المفتوحة عبر أربع مراحل مترابطة: تحديد مدينة من صورة منزلية، التحقق من تاريخ ظهور موقع مؤرشف، التعرف على معلم ومبنى تاريخي من صورة، ثم استخراج علم من وثيقة داخلية بصيغة ODT. يعتمد المسار على **البيانات الوصفية للصور، وأرشيفات WARC، والبحث العكسي عن الصور، وبيانات المستندات**.[1] [2]

تبدأ الأدلة من منزل يحمل اسم **The Rectory** وعلامة **ADT Armed Response**، ثم تنتقل إلى أرشيف موقع ACME Jet Solutions، وبعد ذلك إلى صورة معلم في دبلن، وتنتهي باسم مستخدم مخفي داخل وثيقة ODT يقود إلى قناة YouTube. النتيجة النهائية هي قبول أربعة أعلام داخل TryHackMe.

## مسار الحل

### 1. المهمة الأولى — The Leaked Photo

تُظهر الصورة منزلاً سكنياً يحمل لوحة `The Rectory` على البوابة، إضافة إلى علامة `ADT Armed Response`. هذه العلامات تضيق نطاق البحث جغرافياً، بينما تساعد بيانات EXIF في اختبار الموقع المقترح. الإحداثيات المستخرجة من الملف هي:

```text
Latitude: 26° 12′ 14.76″ S
Longitude: 28° 02′ 50.28″ E
```

تقود الإحداثيات إلى **Johannesburg** في جنوب أفريقيا، وهو ما يتسق مع قرينة ADT الظاهرة في الصورة.[2] [3]

الصيغة التي قبلتها المنصة:

```text
THM{Johannesburg}
```

### 2. المهمة الثانية — Archived Company Website

تدّعي ACME Jet Solutions أنها تأسست في عام 2025، لكن السؤال يطلب التحقق من أول ظهور للموقع `warc-acme.com/jef/` باستخدام مصادر عامة. عدم ظهور نتيجة مفيدة في البحث الاعتيادي لا يعني عدم وجود نسخة مؤرشفة؛ فامتداد WARC يشير إلى **Web ARChive**، وهو تنسيق يُستخدم لحفظ لقطات الويب.[2] [4]

يُراجع أرشيف WARC الخاص بالموقع، ثم يُؤخذ timestamp لأول ملف في الالتقاط. القيمة المطلوبة هي:

```text
20160210224602
```

وبما أن صيغة السؤال تتطلب العلم كاملاً، كانت الإجابة المقبولة:

```text
THM{20160210224602}
```

### 3. المهمة الثالثة — Mysterious Landmark

تُظهر الصورة معلماً معروفاً في دبلن، وتحدد المقارنة البصرية والبحث العكسي المعلم بأنه **Spire of Dublin**، المعروف أيضاً باسم **Millennium Spire**.[2] [6]

يطلب وصف المهمة إرسال اسم المبنى الواقع إلى يمين المعلم، وهو مبنى لعب دور مهم في نضال أيرلندا من أجل الاستقلال. المبنى هو **General Post Office (GPO)**، وكان مقراً رئيسياً خلال انتفاضة عيد الفصح عام 1916.[2]

العلم المقبول في حقل الإجابة هو:

```text
THM{General Post Office}
```

> **تمييز مهم:** المعلم الظاهر في الصورة هو `Spire of Dublin`، أما الإجابة المطلوبة في المنصة فهي اسم المبنى المجاور `General Post Office`.

### 4. المهمة الرابعة — Internal Documents

تتضمن المهمة وثيقة داخلية بصيغة ODT. قد يبدو النص المرئي عادياً، لكن ملف ODT عبارة عن حزمة ZIP تحتوي ملفات XML وبيانات وصفية. بعد فحص البيانات الداخلية تظهر قيمة اسم مستخدم:

```text
markwilliams7243
```

يقود البحث عن اسم المستخدم إلى قناة YouTube عامة، ويحتوي المنشور الوحيد فيها على العلم النهائي.[2] [5]

العلم الذي قبلته المنصة هو:

```text
THM{Y0u_f0und_7h3_fin4l_fl4g!}
```

## الإجابات النهائية

| # | المهمة | الإجابة المقبولة |
|---:|---|---|
| 1 | The Leaked Photo — In which city was the photo taken? | `THM{Johannesburg}` |
| 2 | Archived Company Website — When was the website first published on the internet? | `THM{20160210224602}` |
| 3 | Mysterious Landmark — What is the landmark? | `THM{General Post Office}` |
| 4 | Internal Documents — What is the final flag? | `THM{Y0u_f0und_7h3_fin4l_fl4g!}` |

## التحقق الرسمي داخل TryHackMe

تم إدخال الإجابات الأربع في الحقول الرسمية للغرفة، وظهرت عبارة **Correct Answer** لكل مهمة. بعد التحقق من العلم الأخير انتقلت الصفحة إلى مسار الإكمال:

```text
https://tryhackme.com/room/osintchallengeiv/congratulations?step=records
```

وظهرت الرسالة `Great work 9gkc! Room completed!` مع أربع مهام مكتملة و120 نقطة. لم يتم إرسال تقييم الغرفة، ولم يتم الضغط على **Submit now**.

## الدروس الأمنية

توضح الغرفة أن الصورة قد تكشف الموقع من خلال EXIF أو من خلال تفاصيل تبدو هامشية مثل لوحة منزلية وشعار شركة أمنية. كما أن امتداد WARC قد يكون دليلاً على وجود نسخة محفوظة خارج Wayback Machine، وأن ملفات المكاتب الحديثة قد تحتوي على بيانات وصفية لا تظهر في النص المرئي. لذلك ينبغي إزالة البيانات الوصفية الحساسة قبل نشر الصور والمستندات، ومراجعة هوية مؤلفي commits والملفات، وعدم افتراض أن حذف النص الظاهر يحذف كل المعلومات المضمنة.

أما في التحقيقات الواقعية، فيجب إبقاء البحث ضمن نطاق قانوني واضح، وعدم استخدام أسماء المستخدمين أو الوثائق العامة للتواصل مع أشخاص أو اختبار حسابات دون تفويض صريح.

## المراجع

[1]: https://tryhackme.com/room/osintchallengeiv "TryHackMe — Digital Footprint"
[2]: https://syswraith.com/blog/ctfs/digital-footprint "Digital Footprint — TryHackMe Write-up"
[3]: https://ta1al.com/blog/digital-footprint-tryhackme-writeup/ "Digital Footprint — TryHackMe Room Writeup"
[4]: https://archive.org/details/warc-acme.com-jef "Internet Archive — warc-acme.com/jef WARC capture"
[5]: https://www.youtube.com/@markwilliams7243 "YouTube channel referenced by the challenge path"
[6]: https://maps.app.goo.gl/WBR6aSFipPG7wGTR9 "Google Maps location reference for Johannesburg image analysis"
