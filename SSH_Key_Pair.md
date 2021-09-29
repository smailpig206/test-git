# SSH_Key_Pair
## Tổng quan
### SSH Key là gì
Là một phương thức chứng thực người dùng bằng cách đối chiếu một khóa cá nhân (Private Key) với khóa công khai(Public Key). Private key và Public key có môits liên hệ chặt chẽ với nhau nhằm mục đích nhận diện lẫn nhau.
### Thành phần
SSH Key pair có 3 thành phần chính:
* Public key(dạng file và string): có thể lấy ở bất kì server nào.Với linux sẽ được lưu trong  ~/.ssh/authorized_keys
* Private key(dạng file và string):lưu trữ trên máy tính.
* Keyphrase(dạng string, cần ghi nhớ): mật khẩu để mở private key.
### Ưu điểm
* SSH Key khó bị hack và an toàn hơn mật khẩu
* Kết nối SSH chỉ có thể đến từ máy tính có chứa private key
* CHo phép nhiều người đăng nhập với cùng tên người dùng mà không phải chia sẻ mật khẩu
* Có thể thu hồi quyền truy cập của bất kì ai
* Giúp đăng nhập vào nhiều tài khoản SSH dễ dàng mà không cần quản lý nhiều mật khẩu
* Cho phép thêm mật khẩu cho xác thực SSH key để tăng tính bảo mật
### Nhược điểm
* Private key cần lưu trữ trên thiết bị mà bạn đăng nhập nên nếu mất máy sẽ rất nguy hiểm
* Thiết lập SSH cần nhiều thao tác
* Việc phân phối Public key và hướng dẫn SSH key sẽ phức tạp
## Cách hoạt động
![image](https://nhanhoa.com/uploads/attach/1624070125_ssh-key-la-gi-3.png)
## Tạo SSH Key
Bước 1: Tạo ssh key trên client
```
ssh-keygen -t rsa
```
![sshkeygen](https://i.imgur.com/eDI7Hh4.png)

 * Check private key da tao
 ```
 cat /roor/.ssh/id_rsa
 ```
![sshprivate](https://i.imgur.com/Kekzn4n.png)
* Tương tự với public key
 ```
 cat /roor/.ssh/id_rsa.pub
 ```
Bước 2: Copy public key tới máy chủ
  ```
  ssh-copy-id -i ~/.ssh/id_rsa 192.168.141.129
  ```
Bước 3 : Đăng nhập kiểm tra
## Tài liệu tham khảo
[SSH Key là gì? Cách sử dụng SSH Key](https://wiki.tino.org/ssh-key-la-gi/)