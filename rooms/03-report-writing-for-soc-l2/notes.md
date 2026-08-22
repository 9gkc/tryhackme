# ملاحظات حل غرفة Report Writing for SOC L2

الرابط: https://tryhackme.com/room/reportwritingsocl2

تم الانضمام إلى الغرفة، وTask 1 مفتوح. السؤال هو `Let's go!` ولا يحتاج إجابة نصية؛ سيتم تأكيده باستخدام Check.

المهام الظاهرة بعد الانضمام:
- Task 1: Introduction
- Task 2: L1 vs L2 Communication
- Task 3: Leadership Communication — يحتوي تحديًا تفاعليًا عبر View Site.
- Task 4: SOC/DFIR Communication — يحتوي تحديًا تفاعليًا عبر View Site.
- Task 5: Responsible AI Usage
- Task 6: Conclusion

من محتوى الغرفة: L2 يربط SOC بالعالم الخارجي، ويكتب تقارير case summary وMSSP email وDFIR handover notes. قنوات التواصل تشمل voice call للحالات العاجلة، email للتحديثات الأمنية مع CC، ticketing system للعملاء، وcorporate chat للنقاشات الداخلية.

تم إكمال Task 1 بنجاح، وأصبح تقدم الغرفة 8%. محتوى Task 2 يوضح أن L2 هو المستوى الذي يربط SOC بالعالم الخارجي، وأن L2 يكتب reports لتلخيص نتائج SOC. الإجابات المتوقعة: `L2` و`Reports`.

تم التحقق من إجابات Task 2 (`L2` و`Reports`) بنجاح، وأصبح تقدم الغرفة 25%. تبقى Task 3 — Leadership Communication — وهي تتضمن تحديًا تفاعليًا وسؤالين إضافيين.

Task 3 — Leadership Communication يحتوي ثلاثة أسئلة بعد التحدي:
- Should you complete the analysis after sharing the initial SOC report? (Yea/Nay) — الإجابة المتوقعة `Yea`، لأن التقرير الأولي يبدأ الاحتواء ولا يغني عن استكمال التحقيق.
- Should you keep your team informed about the ongoing communication? (Yea/Nay) — الإجابة المتوقعة `Yea`.
- What flag did you receive after completing the task's challenge? — سيُستخرج من التطبيق.

تم إكمال تحدي C-Level Communication بنتيجة 5/5، وظهر العلم: `THM{executive_summary_approved}`. تصنيفات الأجزاء الخاطئة كانت: Missing recipient، Missing context، Excessive response، Unclear timeline، Unprofessional language.

تم إكمال تحدي C-Level Communication بنتيجة 5/5، وظهر العلم `THM{executive_summary_approved}`. إجابات Task 3 المتوقعة: `Yea` لاستكمال التحليل بعد التقرير الأولي، و`Yea` لإبقاء الفريق على اطلاع أثناء التواصل المستمر.

تم فتح Task 4 — SOC/DFIR Communication — وأصبح تقدم الغرفة 50%. الأسئلة هي: `Are L2 handover notes meant for a non-technical audience? (Yea/Nay)` وإجابتها `Nay`؛ و`What part of the handover notes lists your findings chronologically?` وإجابتها `Attack Timeline`؛ إضافة إلى علم التحدي الذي سيُستخرج من التطبيق.

تطبيق Task 4 المباشر: https://static-labs.tryhackme.cloud/apps/soc-l2-report-dfir/

التصنيفات الصحيحة للأجزاء المظللة في تحدي DFIR هي: `Unnecessary text` للعبارة but given the overall nature of the circumstances surrounding the incident؛ `Ambiguous phrasing` للعبارة OT environment may have been affected in some way؛ `Missing actor` للعبارة was executed؛ `No evidence` للعبارة was exfiltrated؛ و`Missing context` للعنصر Other IPs. العلم الموجود في منطق التطبيق هو `THM{trysaveme_would_be_proud}`.
