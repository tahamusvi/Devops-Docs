
با این دستوره میشه لاجیکال والیوم ساخت 
sudo lvcreate -n lv_redis -l 100%FREE vg_redis



با این دستور هم فایل سیستم رو میسازیم روش
sudo mkfs.ext4 /dev/vg_redis/lv_redis

بعدش هم باید با دستور زیر ایدیش رو بگیری

sudo blkid /dev/vg_redis/lv_redis


بعدش این خط رو تو fstab براش اضافه میکنی.


UUID=1234abcd-56ef-7890-1234-56789abcdef0  /srv/redis  ext4  defaults  0  2
