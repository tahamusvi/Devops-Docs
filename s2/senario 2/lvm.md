اول از همه lvm یه سیستم مدیریت حافظه میشه گفت هستش که بهمون اجازه میده فضای چندتا دیسک رو ترکیب کنیم و حجم ها رو داینمیک و بدون فرمت مجدد بزرگ و کوچیک کنیم



برای شروع کار sdb رو تبدیل به PV یا فیزیکال والیوم میکنیم.
sudo pvcreate /dev/sdb



sudo vgcreate vgdata /dev/sdb
با این دستور یه Volume Group می سازیم.


vgs
 برای تست اینو میزنیم




sudo lvcreate -l 100%FREE -n lvdata vgdata
lvs

 به نام `lvdata` با کل فضای آزاد ساخته می‌شه.


sudo mkfs.ext4 /dev/vgdata/lvdata



sudo mkdir -p /data


sudo mount /dev/vgdata/lvdata /data



دقیقا مثل همون مانت معمولی عمل میکنیم

sudo blkid /dev/vgdata/lvdata

UUID=abcd-1234-efgh-5678 /data ext4 defaults 0 2

sudo umount /data
sudo mount -a