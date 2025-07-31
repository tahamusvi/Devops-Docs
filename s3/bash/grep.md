
global regular expression print




grep -i "error" t.txt
پیدا کردن error بدون توجه به کوچیک بزرگی

grep -iv "debug" t.txt
فلگ V میشه برعکس کردن یعنی اونایی شامل دیباگ نیستن


grep -iE "info|warning" t.txt
اینجوری هم میتونیم رجکس بدیم

grep -in "debug" t.txt

شماره خط هارو میزاره

grep -ic "debug" t.txt

تعداد تطابق هارو میده

grep -io "debug" t.txt
فقط کلمه تطابق رو میده