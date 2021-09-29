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
    - [Employing	Multiple	Screens](#employingmultiplescreens)
    - [Understanding	Foreground	and Background	Processes](#understandingforegroundand-backgroundprocesses)
    - [Managing	Process	Priorities](#managingprocesspriorities)
    - [Sending	Signals	to	Processes](#sendingsignalstoprocesses)
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
| Short | Long | Description |
| ----- | ---- | ----------- |
| -e    |--erase| xóa bỏ phần mềm được chỉ định         |
| -F    |--freshen      |Cập nhật nếu phiên bản mới nhất đã có             |
| -i    |--install      |Cài đặt gói tin được chỉ định             |
| -q    |--query      |Truy vấn gói tin được chỉ định có được cài đặt hay không             |
| -U    |--upgrade      |Cài đặt hoặc cập nhật gói tin được chỉ định             |
| -v    |--verify      |xác định tính tồn tại và tính toàn vẹn của gói tin           |
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
### Using	ZYpp 
## Using	Debian	Packages 
### Debian	Package	File	Conventions 
### The	`dpkg`	Command	Set 
### Looking	at	the	APT	Suite 
### Using	`apt-cache `
### Using	`apt-get `
### Reconfiguring	Packages 
## Managing	Shared	Libraries 
### Library	Principles 
### Locating	Library	Files 
### Loading	Dynamically 
### Library	Management	Commands 
## Managing	Processes 
### Examining	Process	Lists 
### Employing	Multiple	Screens 
### Understanding	Foreground	and Background	Processes 
### Managing	Process	Priorities 
### Sending	Signals	to	Processes