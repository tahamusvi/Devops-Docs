
باید Network Adapter را روی Bridged باید بزاریم.


sudo nano /etc/netplan/50-cloud-init.yaml
بعد این فایله رو تغییر میدیم


network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: false
      addresses:
        - 192.168.1.200/24
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
      routes:
        - to: 0.0.0.0/0
          via: 192.168.1.1


اعمال کردن کانفیگ

sudo netplan apply



تست اتصال
ip a              # بررسی IP
ip r              # بررسی route
ping 8.8.8.8      # تست اینترنت
ping google.com   # تست DNS



sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh
