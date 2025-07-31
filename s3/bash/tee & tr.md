

دستور tr برای عوض کردن کاراکتر ها هستش translate

به این شکل مثلا
echo "hello world" | tr 'a-z' 'A-Z'
 خروجی: HELLO WORLD


echo "user@name!" | tr -d '@!'
 خروجی: username


echo "aaabbbbcc" | tr -s 'a-z'
خروجی: abc


 دستور tee برای ذخیره سازی نتیجه دستور تو فایل هستش در عین حال Stdout شه

ls -l | tee list.txt


tman@Lg1:~/learn-cat$ echo "127.0.0.1    mylocal.dev" | sudo tee -a /etc/hosts
127.0.0.1    mylocal.dev