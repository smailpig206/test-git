Bước 1: Vào /etc/ssh/sshd_config
```
vim /etc/ssh/sshd_config
```
Bước 2: Tìm dòng `PermitRootLogin` chỉnh `yes` thành `no`.
![no](https://i.imgur.com/DZcXHk7.png)
Bước 3: Restart sshd.service
```
systemctl restart sshd.service
```
Bước 4: Check lại
![denied root](https://i.imgur.com/SGFeSM4.png)
Thử với user khác![user kahcs](https://i.imgur.com/ZMAnjx1.png)