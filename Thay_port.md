* Bước 1 . Vào file sshd_config
  ```
  vim /etc/ssh/sshd_config
  ```
* Bước 2: SELinux chỉ cho ssh hoạt động ở cổng 22. Cài đặt Semanage
  ```
  yum -y install  policycoreutils-python
  ```
  Check cổng SSH hiện tại
  ![sshportcu](https://i.imgur.com/eswdd9h.png)
* Bước 3: CHỉnh port 
  ![chinhportdung](https://i.imgur.com/9zrS4WY.png)
  Ta có thể xóa port cũ với lệnh
  ```
  [root@localhost ~]# semanage port -d -t ssh_port_t -p tcp 22
  ```

* Bước 4: Restart SSH service
  ![restart ssh](https://i.imgur.com/e2WunO8.png)
* Bước 5: Thêm port vào firewall và reload firewall
  ![reload](https://i.imgur.com/vNBxYgM.png)
* Bước 6: Check lại
  ![checklai](https://i.imgur.com/aNplJPJ.png)







  Tài liệu tham khảo
  * [https://sharadchhetri.com/centos-7-rhel-7-change-openssh-port-number-selinux-enabled/](https://sharadchhetri.com/centos-7-rhel-7-change-openssh-port-number-selinux-enabled/)
  * [https://helpdesk.inet.vn/knowledgebase/huong-dan-doi-port-ssh-mac-dinh-tren-centos-7-minimal](https://helpdesk.inet.vn/knowledgebase/huong-dan-doi-port-ssh-mac-dinh-tren-centos-7-minimal)
  