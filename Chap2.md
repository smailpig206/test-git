# Chap 2
Mục lục
- [Chap 2](#chap-2)
  - [Looking	at	Package	Concepts](#lookingatpackageconcepts)
  - [Using	RPM](#usingrpm)
    - [RPM	Distributions and Conventions](#rpmdistributions-and-conventions)
    - [The	`rpm` Command Set](#therpm-command-set)
      - [Installing and Updating RPM Packages](#installing-and-updating-rpm-packages)
      - [Query RPM packages](#query-rpm-packages)
      - [Verifying RPM Packages](#verifying-rpm-packages)
      - [Removing RPM Packages](#removing-rpm-packages)
    - [Extracting	Data	from	RPMs](#extractingdatafromrpms)
    - [Using	YUM](#usingyum)
    - [Using	ZYpp](#usingzypp)
  - [Using	Debian	Packages](#usingdebianpackages)
    - [Debian	Package	File	Conventions](#debianpackagefileconventions)
    - [The	`dpkg`	Command	Set](#thedpkgcommandset)
    - [Looking	at	the	APT	Suite](#lookingattheaptsuite)
    - [Using	`apt-cache `](#usingapt-cache-)
    - [Using	`apt-get `](#usingapt-get-)
    - [Reconfiguring	Packages](#reconfiguringpackages)
  - [Managing	Shared	Libraries](#managingsharedlibraries)
    - [Library	Principles](#libraryprinciples)
    - [Locating	Library	Files](#locatinglibraryfiles)
    - [Loading	Dynamically](#loadingdynamically)
    - [Library	Management	Commands](#librarymanagementcommands)
  - [Managing	Processes](#managingprocesses)
    - [Examining	Process	Lists](#examiningprocesslists)
      - [Viewing Process with `ps`](#viewing-process-with-ps)
      - [Selecting Process with `ps`](#selecting-process-with-ps)
      - [Viewing Process with `top`](#viewing-process-with-top)
    - [Employing	Multiple	Screens](#employingmultiplescreens)
      - [Multiplexing with `tmux`](#multiplexing-with-tmux)
    - [Understanding	Foreground	and Background	Processes](#understandingforegroundand-backgroundprocesses)
      - [Sending  a Job to the Background](#sending--a-job-to-the-background)
    - [Stopping a Job](#stopping-a-job)
## Looking	at	Package	Concepts 
Có 2 trình quản lý package hay dùng
* Red Hat package management(RPM)
* Debian package management(Apt)
Các trình quản lý theo dõi các thông tin :
* Tệp ứng dụng
* Thư viện đi kèm
* Phiên bản của ứng dụng
## Using	RPM 
### RPM	Distributions and Conventions 
RPM package có phần mở rộng .rpm và đặt tên theo định dạng này:
```
PACKAGE-NAME-VERSION-RELEASE.ARCHITECTURE.rpm
```
Trong đó
* Package-name: là tên gói phần mềm
* Version: phiên bản của chương trình
* Release: hay build number.Nó đại diện cho 1 chương trình sửa đổi nhỏ hơn so với phiên bản.
* Architecture: là chỉ định kiến trúc CPU mà phần mềm được tối ưu hóa.
Syntax:
```
rpm [ACTION] [OPTION] PACKAGE-FILE
```
Check các gói rpm đã cài trong máy
```
[root@hoanganh ~]# ls -l *.rpm
-rw-r--r--. 1 root root 2846724 Nov 18  2020 httpd-2.4.6-97.el7.centos.x86_64.rpm
```
Hoặc kiểm tra trực tiếp tên phần mềm nào đó với option `-q`
```
[root@hoanganh ~]# rpm -q docker
package docker is not installed
```
### The	`rpm` Command Set 
Một số option hay dùng
| Short | Long      | Description                                              |
| ----- | --------- | -------------------------------------------------------- |
| -e    | --erase   | xóa bỏ phần mềm được chỉ định                            |
| -F    | --freshen | Cập nhật nếu phiên bản mới nhất đã có                    |
| -i    | --install | Cài đặt gói tin được chỉ định                            |
| -q    | --query   | Truy vấn gói tin được chỉ định có được cài đặt hay không |
| -U    | --upgrade | Cài đặt hoặc cập nhật gói tin được chỉ định              |
| -v    | --verify  | xác định tính tồn tại và tính toàn vẹn của gói tin       |
#### Installing and Updating RPM Packages
Option `-vh` sẽ hiển thị quá trình update và cái gì đang chạy

```
[root@hoanganh ~]# rpm -Uvh zsh-5.0.2-34.el7_8.2.x86_64.rpm
Preparing...                          ################################# [100%]
Updating / installing...
   1:zsh-5.0.2-34.el7_8.2             ################################# [100%]
```
#### Query RPM packages
Thực hiện truy vấn chi tiết 1 gói RPM
```
[root@hoanganh ~]# rpm -qi zsh
Name        : zsh
Version     : 5.0.2
Release     : 34.el7_8.2
Architecture: x86_64
Install Date: Thu 23 Sep 2021 05:38:59 PM +07
Group       : System Environment/Shells
Size        : 5860430
License     : MIT
Signature   : RSA/SHA256, Wed 08 Apr 2020 09:41:00 PM +07, Key ID 24c6a8a7f4a80eb5
Source RPM  : zsh-5.0.2-34.el7_8.2.src.rpm
Build Date  : Tue 07 Apr 2020 09:38:13 PM +07
Build Host  : x86-02.bsys.centos.org
Relocations : (not relocatable)
Packager    : CentOS BuildSystem <http://bugs.centos.org>
Vendor      : CentOS
URL         : http://zsh.sourceforge.net/
Summary     : Powerful interactive shell
Description :
The zsh shell is a command interpreter usable as an interactive login
.....
```
#### Verifying RPM Packages
Theo dõi các gói tin để đảm bảo an toàn hệ thống. Nếu kêt quả trả về là rỗng hoặc một dấu chấm, đó là điều tốt.
```
[root@hoanganh ~]# rpm -V zsh
[root@hoanganh ~]
```
#### Removing RPM Packages
Option `-e`
```
[root@hoanganh ~]# rpm -e zsh
[root@hoanganh ~]# rpm -q zsh
package zsh is not installed
```
### Extracting	Data	from	RPMs 
`rom2cpio` là giúp giải nén tệp rpm mà không cần cài đặt nó. Điều duy nhất cần chú ý là cần điều hướng đầu ra với kí tự `>` để tạo file lưu trữ
```
[root@hoanganh ~]# rpm2cpio emacs-24.3-23.el7.x86_64.rpm > emacs.cpio
```
Sau khi tạo file   `.cpio` ta giải nén file vào các thư mục với các option `-i` để copy, `-d` để tạo các thư mục con trong thư mục hiệN tại, `-v` để hiện thêm thông tin
```
[root@hoanganh ~]# cpio -idv < emacs.cpio
./usr/bin/emacs-24.3
./usr/share/applications/emacs.desktop
./usr/share/applications/emacsclient.desktop
./usr/share/icons/hicolor/128x128/apps/emacs.png
./usr/share/icons/hicolor/16x16/apps/emacs.png
./usr/share/icons/hicolor/24x24/apps/emacs.png
./usr/share/icons/hicolor/32x32/apps/emacs.png
./usr/share/icons/hicolor/48x48/apps/emacs.png
./usr/share/icons/hicolor/scalable/apps/emacs.svg
./usr/share/icons/hicolor/scalable/mimetypes/emacs-document.svg
29284 blocks
[root@hoanganh ~]# 
```
### Using	YUM 
YUM là công cụ làm việc với kho lưu tữ Red Hat(`YellowDog Update Manager`), cho phép bạn truy vấn, cài đặt, và xóa các gói phần mềm trực tiêp trên hệ thống của bạn qua kho lưu trữ chính của Red Hat
Xem các tệp kho lưu trữ trong /etc/yum.repos.d/
```
[root@hoanganh ~]# ls /etc/yum.repos.d/
CentOS-Base.repo  CentOS-Debuginfo.repo  CentOS-Media.repo    CentOS-Vault.repo
CentOS-CR.repo    CentOS-fasttrack.repo  CentOS-Sources.repo  CentOS-x86_64-kernel.repo
```
Update
* Kiểm tra cập nhật các ứng dụng đã cài đặt
  ```
  yum check-update
  ```
* Cập nhật các ứng dụng đã cài
    ```
    yum update
    ```
    Hoặc với 1 package cụ thể
    ```
    yum update [package]
    ```
Install
* `-y` cho phép đồng ý với tất cả yêu cầu
  ```
  yum -y install [package]
  ```
Remove
  * Xóa gói chỉ định
  ```
  yum remove [package]
  ```
Info
  * Xem thông tin
  ```
  yum info [package]
  ```
### Using	ZYpp 
Bản phân phối `openSUSE` cũng sử dụng hệ thống quản lý gói RPM và phân phối dưới dạng tệp `.rpm` nhưng không sử dụng công cụ `yum` hay `dnf`. Thay vào đó họ sử dụng `ZYpp`. Nhìn chung câu lệnh khá giống với `yum`.

## Using	Debian	Packages
### Debian	Package	File	Conventions 
Debian đóng gói các file phần mềm dưới dạng `.deb`, thường được sử dụng trên các bản phân phối Linux dựa trên Debian, ví dụ như Ubuntu
 ```
 PACKAGE-NAME-VERSION-RELEASE_ARCHITETURE.deb
 ```
### The	`dpkg`	Command	Set
 Syntax:
 ```
 dpkg [OPTIONS] ACTION PACKAGE-FILE 
 ```
 Cài đặt gói `.deb` với tham số `-i`
 ```
Selecting previously unselected package zsh.
(Reading database ... 171250 files and directories currently installed.)90 Chapter 
Preparing to unpack zsh_5.4.2-3ubuntu3.1_amd64.deb ...
Unpacking zsh (5.4.2-3ubuntu3.1) ...

 ```
 Tham số `-l` để hiện các gói đã cài đặt
 ```
 $ dpkg -l
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name Version Architecture Description
+++-==============-============-============-===========================
ii accountsservic 0.6.45-1ubun amd64 query and manipulate accounts
ii acl 2.2.52-3buil amd64 Access control list utilities
ii acpi-support 0.142 amd64 scripts for handling ACPI
ii acpid 1:2.0.28-1ub amd64 Advanced Config and Power
ii adduser 3.116ubuntu1 all add and remove users
[…]
iU zsh 5.4.2-3ubunt amd64 shell with lots of features
$
 ```
### Looking	at	the	APT	Suite 
### Using	`apt-cache `
Tìm gói đã được cài với `apt-cache pkgnames`
```
$ apt-cache pkgnames | grep ^nano
nano
[…]
nano-tiny
[…]
$
```
Hiển thị thông tin của gói
```
$ apt-cache showpkg zsh
Package: zsh
Versions:
5.4.2-3ubuntu3.1 […]
[…]
```
### Using	`apt-get `
Tương tự như `yum`, `apt-get` được sử dụng để cài đặt, cập nhật và xóa các gói từ 1 kho lưu trữ gói Debian.
Cài đặt 1 gói với lệnh `apt-get install`
```
$ sudo apt-get install zsh
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
zsh-common
...
```
### Reconfiguring	Packages
Hiển thị cấu hình gói cài đặt
 ```
 $ sudo debconf-show cups
* cupsys/backend: lpd, socket, usb, snmp, dnssd
* cupsys/raw-print: true
$
 ```
## Managing	Shared	Libraries 
### Library	Principles 
### Locating	Library	Files 
### Loading	Dynamically 
### Library	Management	Commands 
## Managing	Processes 
### Examining	Process	Lists 
Khi hệ thống Linux bắt đầu chạy, nó sẽ khởi động 1 process đặc biệt gọi là `init process`. `init` là nhân của hệ thống Linux, nó sẽ chạy tập lệnh khởi động tất cả các quá trình khác.
#### Viewing Process with `ps`
`ps` command
![pscommand](https://i.imgur.com/G3DeGa7.png)
Xem các chương trình đang chạy với Unix-style 
![ps -ef](https://i.imgur.com/fHRxCmG.png)
* UID: Người dùng đang chạy tiến trình
* PID: ID của tiến trình
* PPID: ID của tiến trình mẹ nếu nó được sinh ra từ tiến trình khác
* C : Việc sử dụng bộ xử lý trong suốt thời gian tồn tại của quá trình
* STIME: Thời gian hệ thống bắt đầu tiến trình
* TTY: Thiết bị đầu cuối mà từ đó tiến trình được bắt đầu
* TIME: Thời gian chuẩn bị cpu cần thiết để chạy tiến trình
* CMD: Tên chương trình bắt đầu tiến trình này
#### Selecting Process with `ps`
```
[hoanganh@localhost ~]$ ps -u hoanganh
   PID TTY          TIME CMD
  2042 ?        00:00:00 sshd
  2043 pts/0    00:00:00 bash
  2062 ?        00:00:00 sshd
  2067 ?        00:00:00 sftp-server
  2220 pts/0    00:00:00 ps
[hoanganh@localhost ~]$
```
#### Viewing Process with `top`
`top` sẽ giải quyết một số vấn đề mà `ps` không hỗ trợ, chẳng hạn bạn cố gắng tìm quá trình nào đó thường xuyên hoán đổi trong và ngoài bộ nhớ.`top` cập nhật theo thời gian thức(real-time)
![top1](https://i.imgur.com/pkomC3Y.png)
Khu vực đầu tiên của `top` hiển thị các thông tin cơ bản của hệ thống. DÒng đầu tiên show thời gian hiện tại, thời gian hệ thống đã hoạt động, số ượng user đã đăng nhập và thời gian load trung bình của hế thống
Khu thứ 2 hiển thị chi tiết trạng thái bộ nhớ hệ thống: trạng thái, tổng , đang dùng hiện tại, trống bao nhiêu ....
Khu tiếp theo của công cụ `top` hiển thị chi tiết danh sách các chương trình hiện tại đang chạy
* PID: ID của process
* USER: tên của người đang chạy process
* PR: Mức độ ưu tiên của quá trình
* NI: Giá trị tốt cảu process
* VIRT: Tổng số lượng bộ nhớ ảo đã dùng của process
* RES: Tổng số lượng bộ nhớ vật lý mà process đang dùng
* SHR: Số lượng bộ nhớ mà process này đang chia sẻ với process khác
* S: Trạng thái của process(D: interuptible sleep,I=idle,R=Running,S=Sleeping,T=TRaced of stopped and Z = zombie)
### Employing	Multiple	Screens 
Công cụ `screen` tạo thêm của số làm việc
#### Multiplexing with `tmux`
`tmux` tương tự như `screen` tuy nhiên nó được cải tiến với một số chức năng hữu ích khác.Cả 2 công cụ không được cài đặt sẵn trong hệ thống.
### Understanding	Foreground	and Background	Processes 
#### Sending  a Job to the Background

### Stopping a Job
Lệnh  `kill` cho phép dừng 1 background job
```
$ jobs -l
[1]- 1539 Running sleep 3000 &
[2]+ 1540 Running bash CriticalBackups.sh &
$
$ kill %1
[1]- Terminated sleep 3000
```
