# LPIC
Mục lục
- [LPIC](#lpic)
  - [Exploring Your Linux Shell Options](#exploring-your-linux-shell-options)
  - [Using a shell](#using-a-shell)
  - [Các siêu kí tự trích dẫn](#các-siêu-kí-tự-trích-dẫn)
  - [Khám phá cấu trúc thư mục](#khám-phá-cấu-trúc-thư-mục)
  - [Tìm hiểu lệnh](#tìm-hiểu-lệnh)
  - [Sử dụng biến môi trường(Environment Variables)](#sử-dụng-biến-môi-trườngenvironment-variables)
  - [Geting help](#geting-help)
- [Editing Text Files](#editing-text-files)
  - [Một số lệnh di chuyển](#một-số-lệnh-di-chuyển)
  - [Một số lệnh chỉnh sửa](#một-số-lệnh-chỉnh-sửa)
  - [Lệnh vim trong chế độ Ex](#lệnh-vim-trong-chế-độ-ex)
  - [Lưu thay đổi](#lưu-thay-đổi)
- [Processing Text Using Filters](#processing-text-using-filters)
  - [File-Combining Commands](#file-combining-commands)
  - [File-Transforming Commands](#file-transforming-commands)
  - [Phân tách với `split`](#phân-tách-với-split)
  - [File-Formatting Commands](#file-formatting-commands)
    - [Organizing with `sort`](#organizing-with-sort)
  - [File-Viewing Commands](#file-viewing-commands)
    - [Using `more` and `less`](#using-more-and-less)
    - [Looking at files with `head`](#looking-at-files-with-head)
    - [Viewing Files with tail](#viewing-files-with-tail)
  - [File-Summarizing Commands](#file-summarizing-commands)
    - [Counting with `wc`](#counting-with-wc)
    - [Pulling Out Portions with  `cut`](#pulling-out-portions-with--cut)
    - [Discovering Repeated Lines with `uniq`](#discovering-repeated-lines-with-uniq)
    - [Digesting an MD5 Algorithm](#digesting-an-md5-algorithm)
    - [Securing Hash Algorithms](#securing-hash-algorithms)
- [Using Regular Expressions](#using-regular-expressions)
  - [Using `grep`](#using-grep)
  - [Understanding Basic Regular Expressions](#understanding-basic-regular-expressions)
  - [Understanding Extended Regular Expressions](#understanding-extended-regular-expressions)
- [Using Streams, Redirection, and Pipes](#using-streams-redirection-and-pipes)
  - [Redirecting Input and Output](#redirecting-input-and-output)
    - [Handling Standard Input](#handling-standard-input)
    - [Redirecting Standard Error](#redirecting-standard-error)
    - [Regular Standard Input](#regular-standard-input)
  - [Piping Data between Programs](#piping-data-between-programs)
    - [Using `sed`](#using-sed)
    - [Generating Command Line](#generating-command-line)
## Exploring Your Linux Shell Options
* Check which shell the file is linked to
```
    readlink /bin/sh
```
    
* Display the current shell on a Centos Distribution
```
    $ echo $SHELL
    /bin/bash
```
    
```
    uname
    uname -r (revision)
    uname -a
```
 ## Using a shell
 * For example with `echo` comnand
 ```
    echo [Option]  [String] ....
 ```
 ## Các siêu kí tự trích dẫn
 * Trong Bash shell có rất nhiều kí tự có ý nghĩa và chức năng đặc biệt. Chúng được gọi là các siêu ký tự trích dẫn(quoting metacharacters).
 ```
    * ? [ ] ' " \ $ ; & ( ) | ^ < >
 ```
 * Ví dụ , kí tự `$` biểu thị rằng kí tự này đi cùng với 1 tên biến. Sử dụng lệnh `echo`, chương trình sẽ cố gắng chạy và hiện thị giá trị của biến.
```
    $ echo $SHELL
    /bin/bash

```

```
    $ echo It cost $1.00
    It cost .00
```
* Do kí tự ```$```, lệnh ```echo``` đối xử với ```$SHELL``` và ```$1``` như là những biến. Trong lệnh thứ 2, ```$1``` không phải l biến và không có giá trị nên đầu ra không hiển thị giá trị nào của ```$1```. Để khắc phục vấn đề này, ta nên mượn *shell quoting*. *Shell quoting* cho phép bạn sử dụng các siêu ký tự như những kí tự thông thường. Để sử dụng shell quote cho 1 kí tự riêng lẻ, ta sử dụng dấu gạch chéo ngược (\- **backslash**)
```
    $ echo It cost \$1.00
    It cost $1.00
```
```
    $ echo Is Schrodinger\'s cat alive or dead\?
    Is Schrodinger's cat alive or dead?
```
* Việc sử dụng backslash đôi khi khá phiền toái khi dùng với nhiều mục tiêu. Thay vào đó có thể dùng ngoặc đơn hoặc ngoặc kép tùy vào từng tình huống
```
    $ echo Is "Schrodinger's" cat alive or "dead?"
    Is Schrodinger's cat alive or dead?
```
```
    $ echo "Is Schrodinger's cat alive or dead?"
    Is Schrodinger's cat alive or dead?
```
```

    $ echo 'Is Schrodinger's cat alive or dead?'
    > ^C
    $
```

* Trường hợp cuối cùng không hoạt động. Khi sử dụng dấu nháy đơn, bảo phải sử dụng thêm các shell quoting khác, ví dụ như backslash hoặc dấu ngoặc kép.

## Khám phá cấu trúc thư mục
* Files trong hệ thống Linux được lưu trữ trong 1 cấu trúc thư mục duy nhất, được gọi là *virtual directory* - thư mục ảo. 
Cấu trúc cây thư mục trong Linux
    * /root
        * /bin
        * /sbin
        * /etc
        * /dev
        * ......

* Sử dụng lệnh ```cd``` và ```pwd```
```
    $ pwd
    /home/hoanganh
```
```
    $ cd /etc
    $ pwd
    /etc
```
* Khi sử dụng lệnh ```cd``` ta có thể sử dụng tham chiếu thư mục tuyệt đối hoặc tương đương. Tham chiếu thư mục tuyệt đối bằng cách sử dụng 1 forward slash (/) và sử dụng tên đầy đủ của vị trí thư mục như trong ví dụ trên
* Tham chiếu thư mục tương đối cho phép di chuyển với lệnh ```cd``` tới một vị trí mới trong cấu trúc thư mục liên quan đến thư mục đang làm việc với cú pháp ngắn hơn
    ```
    $ pwd
    /etc
    $
    $ cd cups
    $ pwd
    /etc/cups
    $
    $ cd ..
    $ pwd
    /etc
    $
    ```
* Lệnh (``` cd ... ```) giúp trở lại thư mục trước. Hai dấu chấm(```..```) đại diện cho thư mục cha của thư mục hiện tại.
* Một số lệnh ```cd``` hay dùng
    * Trở về thư mục home của người dùng
        ```
        cd 
        cd ~
        cd $home
        ```
    * Trở về thư mục sử dụng gần nhất
        ```
        $ pwd
        /etc
        $ cd /var
        $ pwd
        /var
        $
        $ cd -
        /etc
        $ pwd
        /etc
        $
        ```
## Tìm hiểu lệnh
* Sử dụng lệnh  ```type```
    ```
    $ type echo
    echo is a shell built-in
    ```
    ```
    $ type uname
    uname is /usr/bin/name
    ```
## Sử dụng biến môi trường(Environment Variables)
* Biến môi trường theo dõi tin hệ thống cụ thể, như tên người dùng đã đăng nhập vào shell, thư mục home mặc định của người dùng ...
* Một số biến môi trường thông dụng
    ```
    Name            Description
    BASH_VERSION    Current Bash shell instance’s version number 
    EDITOR          Default editor used by some shell commands 
    GROUPS          User account’s group memberships 
    HISTFILE        Name of the user’s shell command history file 
    HISTSIZE        Maximum number of commands stored in history file 
    HOME            Current user’s home directory name 
    HOSTNAME        Current system’s host name 
    LANG            Locale category for the shell 
    LC_*            Various locale settings that override LANG 
    LC_ALL          Locale category for the shell that overrides LANG 
    LD_LIBRARY_PATH Colon-separated list of library directories to search prior to looking
    through the standard library directories 
    PATH            Colon-separated list of directories to search for commands
    PS1             Primary shell command-line interface prompt string 
    PS2             Secondary shell command-line interface prompt string
    PWD             User account’s current working directory 
    SHLVL           Current shell level 
    TZ              User’s time zone, if different from system’s time zone 
    UID             User account’s user identification number 
    VISUAL          Default screen-based editor used by some shell commands
   
    ```
* Sử dụng lệnh ``` set ``` để hiện thị các biến môi trường đang hoạt động
    ```
    $ set
    […]
    BASH=/bin/bash
    […]
    HISTFILE=/home/Christine/.bash_history
    […]
    HISTSIZE=1000
    HOME=/home/Christine
    HOSTNAME=localhost.localdomain
    […]
    PS1='$ '
    PS2='> '
    […]
    SHELL=/bin/bash
    […]
    $
    ```
* Khi nhập tên chương trình tại dấu nhắc shell, shell sẽ tìm tất cả các thư mục được liệt kê trong biến ```PATH``` cho chương trình đó. Nếu không tìm được, nó sẽ thông báo ```command not found```.
* Xem cách  ```PATH``` ảnh hưởng đến việc thực thi lệnh
    ```
    $ echo $PATH
    /usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:
    /home/Christine/.local/bin:/home/Christine/bin
    $
    $ ls /home/Christine/Hello.sh
    /home/Christine/Hello.sh
    $
    $ Hello.sh
    bash: Hello.sh: command not found…
    $ 
    ```
Chương trình `Hello.sh` ở trong thư mục mà nó không nằm trong thư mục của biến môi trường `PATH`. Do đó khi chạy chương trình trong shell prompt, tin nhắn hiện ra là `command not found`.
Lệnh `which` sẽ hữu dụng trong những trường hợp này.Nó thông qua các thư mục của PATH để tìm chương trình
```
$ which Hello.sh
```
![hello.sh](https://i.imgur.com/Tw1EGWo.png)
```
$ which echo
usr/bin/echo

```
Sử dụng các đường dẫn khác nhau để chạy command
```
$ echo Hello World
Hello World
$
$ /usr/bin/echo Hello World
Hello World
$
```
## Geting help
Hệ thống Linux cung cấp 1 chuyên trang gọi là `man pages`. Man pages cung cấp tài liệu về mục đích của lệnh, các tùy chọn, cú pháp ...
Ta có thể tìm từ khóa trong tài liệu bằng option `-k`
```
$ man -k passwd
chgpasswd (8)        - update group passwords in batch mode
chpasswd (8)         - update passwords in batch mode
gpasswd (1)          - administer /etc/group and /etc/gshadow
grub2-mkpasswd-pbkdf2 (1) - Generate a PBKDF2 password hash.
lpasswd (1)          - Change group or user password
pam_localuser (8)    - require users to be listed in /etc/passwd
passwd (1)           - update user's authentication tokens
sslpasswd (1ssl)     - compute password hashes
pwhistory_helper (8) - Helper binary that transfers password hashes from passwd or sha...

```
Lệnh `history` giúp user tìm lại các câu lệnh bạn đã dùng. 
```
$ history
77  man passwd
78  man -k passed
79  man -k passwd
80  man -s 5 passed
81  man -s 5 passwd
82  man  5 passwd
83  man  8  passwd
84  man  1 passwd
85  history

```
Chạy lại command cũ  trong lịch sử command
```
$ !85
77  man passwd
78  man -k passed
79  man -k passwd
80  man -s 5 passed
81  man -s 5 passwd
82  man  5 passwd
83  man  8  passwd
84  man  1 passwd
85  history
```
Chúng ta có thể nhập `!!` để chạy lại command gần nhất.

# Editing Text Files
Vim có 3 chế độ
    * `Command Mode`: Là chế độ khi lần đầu vào vùng đệm. Tại đây bạn nhập các tổ hợp phím để thực hiện lệnh.
    * `Insert Mode`: Hay còn gọi là edit hay entry mode. Ấn phím I để khởi chạy `Insert mode`.
    * `Ex Mode `: Là chế độ mà bất kì lệnh nào đều được bắt đầu với dấu `:`.
##
## Một số lệnh di chuyển
 

| Shortkey | Description                                             |
| :------- | :------------------------------------------------------ |
| h        | Di chuyển sang trái 1 ký tự                             |
| l        | Di chuyển sang phải 1 ký tự                             |
| j        | Di chuyển xuống dưới 1 dòng                             |
| k        | Di chuyển lên trên 1 dòng                               |
| w        | Di chuyển con trỏ về phía trước 1 từ trước từ tiếp theo |
| e        | Di chuyển con trỏ về cuối từ hiện tại                   |
| b        | Di chuyển con về phía sau 1 từ                          |
| ^        | Đưa con trỏ về đầu dòng                                 |
| $        | Đưa con trỏ về cuối dòng                                |
| gg       | Đưa con trỏ về dòng đầu tiên của file                   |
| G        | Di chuyển đến dòng cuối cùng của file                   |
| *n*G     | Di chuyển đến dòng thứ n                                |
| Ctrl+B   | Cuộn lên gần như cả 1 màn hình                          |
| Ctrl+F   | Cuộn xuống gần như cả 1 màn hình                        |
| Ctrl+U   | Cuộn lên nửa màn hình                                   |
| Ctrl+D   | Cuộn xuống nửa màn hình                                 |
| Ctrl+Y   | Cuộn lên 1 dòng                                         |
| Ctrl+E   | Cuộn xuống 1 dòng                                       |


## Một số lệnh chỉnh sửa
| Shortkey | Description                                                     |
| -------- | --------------------------------------------------------------- |
| a        | Chỉnh sửa văn bản sau con trỏ                                   |
| A        | Chèn văn bản vào cuối dòng văn bản                              |
| dd       | Xóa dòng hiện tại                                               |
| dw       | xóa từ hiện tại                                                 |
| i        | Chèn văn bản trưỚc con trỏ                                      |
| I        | Chèn văn bản vào đầu dòng văn bản                               |
| o        | Mở 1 dòng văn bản bên dưới con trỏ và chuyển sang chế độ Insert |
| O        | Mở 1 dòng văn bản bên trên con trỏ và chuyển sang chế độ Insert |
| p        | Paste văn bản đã copy sau con trỏ                               |
| P        | Paste văn bản đã copy trước con trỏ                             |
| yw       | Sao chép từ hiện tại                                            |
| yy       | Sao chép dòng hiện tại                                          |

## Lệnh vim trong chế độ Ex
|             |                                                                               |
| ----------- | ----------------------------------------------------------------------------- |
| :! command  | Khởi tạo shell command và hiển thị kết quả, nhưng không thoát trình soạn thảo |
| :r! command | Khởi tạo shell command và đưa kết quả vào vùng đệm của trình soạn thảo        |
| :r file     | Đọc tiêu đề file và đưa vào vùng đệm của trình soạn thảo                      |
## Lưu thay đổi
| Mode    |      |                                                                        |
| ------- | ---- | ---------------------------------------------------------------------- |
| Ex      | :x   | Ghi bộ đệm vào tệp và thoát trình soạn thảo                            |
| Ex      | :wq  | Ghi bộ đệm vào tệp và thoát trình soạn thảo                            |
| Ex      | :wq! | Ghi bộ đệm vào tệp và thoát trình soạn thảo(overrides protection)      |
| Ex      | :w   | Ghi bộ đệm vào tệp và ở lại trong trình soạn thảo                      |
| Ex      | :w!  | Ghi bộ đệm vào tệp và ở lại trong editor(override protection) |
| Ex      | :q   | Thoát editor nhưng không ghi bộ đệm vào tệp                            |
| Ex      | :q!  | Thoát editor nhưng không ghi bộ đệm vào tệp(overrides protection)      |
| Command | ZZ   | Ghi bộ đệm vào tệp và thoát editor                                     |
# Processing Text Using Filters
## File-Combining Commands
Lệnh `cat` dùng để đọc các file văn bản nhỏ.
Syntax
```
cat [OPTION]... [FILE]...
```
```
[root@hoanganh fuming]# cat hello.sh
 hello
```
Ghép nhiều file bằng `cat `
```
[root@hoanganh fuming]# cat number.txt random.txt
1
3
5
8
99

0.000
hello
VietNam
0101000111
```
Lệnh `paste` giúp hiện thị hai file cạnh nhau (side-to-side)
```
[root@hoanganh fuming]# paste number.txt random.txt
1       0.000
3       hello
5       VietNam
8       0101000111
99
```
## File-Transforming Commands
Lệnh `od` giúp hiện thị văn bản dưới dạng octal(base8), hexadecimal(base16),decimal(base10), and ASCII.
Syntax:
```
od [OPTION]...[FILE]...
```
Ta sẽ thử lệnh `od` để chuyển file về dạng octal
```
[root@hoanganh fuming]# vim testod.txt
[root@hoanganh fuming]# cat testod.txt
Test od command
[root@hoanganh fuming]# od testod.txt
0000000 062524 072163 067440 020144 067543 066555 067141 005144
0000020
```
Dùng `-cb` để biết thêm thông tin
```
[root@hoanganh fuming]# od -cd testod.txt
0000000   T   e   s   t       o   d       c   o   m   m   a   n   d  \n
          25940   29811   28448    8292   28515   28013   28257    2660
0000020

```
## Phân tách với `split`
Lệnh `split` giúp chia file lớn thành các phần nhỏ hơn.
Syntax:
```
split [OPTION]...[FILE]...
```
Dùng option `-l` để chia file bằng số dòng nhất định
```
[root@hoanganh fuming]# cat number.txt
1
3
5
8
99

[root@hoanganh fuming]# split -l 2 number.txt testsplit
[root@hoanganh fuming]# ls -l
total 28
-rw-r--r--. 1 root root  7 Sep 20 10:27 hello.sh
-rw-r--r--. 1 root root 12 Sep 20 17:39 number.txt
-rw-r--r--. 1 root root 31 Sep 20 17:40 random.txt
-rw-r--r--. 1 root root 16 Sep 20 17:53 testod.txt
-rw-r--r--. 1 root root  4 Sep 21 09:18 testsplitaa
-rw-r--r--. 1 root root  4 Sep 21 09:18 testsplitab
-rw-r--r--. 1 root root  4 Sep 21 09:18 testsplitac
[root@hoanganh fuming]# cat testsplitaa
1
3
[root@hoanganh fuming]# cat testsplitab
5
8
[root@hoanganh fuming]# cat testsplitac
99

[root@hoanganh fuming]#

```
## File-Formatting Commands
### Organizing with `sort`
Lệnh `sort` là công cụ để sắp xếp dữ liệu trong file
Ví dụ
```
[root@hoanganh fuming]# cat sorttest.txt
66
17
07
98
52
[root@hoanganh fuming]# sort sorttest.txt
07
17
52
66
98
[root@hoanganh fuming]# sort -n sorttest.txt
07
17
52
66
98
```
Đếm số dòng trong file bằng lệnh `nl`
```
[root@hoanganh fuming]# nl sorttest.txt
     1  45
     2  66
     3  17
     4  07
     5  98
     6  52
     7  36
```
* Thêm option `-ba` để đến tất cả các dòng  
    ```
    [root@hoanganh fuming]# nl -ba sorttest.txt
     1  45
     2  66
     3  17
     4  07
     5  98
     6  52
     7  36
     8
    ```
## File-Viewing Commands
### Using `more` and `less`
Hai lệnh `more` và `less` cho phép người dùng xem văn bản theo tốc độ cuộn tùy chọn.
Syntax:
```
more [OPTION]... [FILE]...
```
```
less [OPTION]... [FILE]...
```
### Looking at files with `head`
Syntax:
```
head [OPTION]... [FILE]...
```
Ví dụ:
```
[root@hoanganh ~]# head /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
```
Lệnh này mặc định sẽ cho bạn chỉ được đọc 10 dòng đầu tiên của file. Thêm option `-n` (hoặc `--lines=`) để chọn số dòng muốn hiển thị.
```
[root@hoanganh ~]# head -n 11 /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
```
### Viewing Files with tail
Trái ngược với `head`, lệnh `tail` sẽ cho bạn xem những dòng cuối của file. Cũng tương tự như `head`, thêm option `-n` để chọn số dòng muốn hiện.
Bên cạnh đó, option `-f` sẽ cho thấy những mục đã nhập vào tệp gần đây nhất
```
$ sudo tail -f /var/log/auth.log
[sudo] password for Christine:
Aug 27 10:15:14 Ubuntu1804 sshd[15662]: Accepted password […]
Aug 27 10:15:14 Ubuntu1804 sshd[15662]: pam_unix(sshd:sess[…]
Aug 27 10:15:14 Ubuntu1804 systemd-logind[588]: New sessio[…]
Aug 27 10:15:50 Ubuntu1804 sudo: Christine : TTY=pts/1 ; P[…]
Aug 27 10:15:50 Ubuntu1804 sudo: pam_unix(sudo:session): s[…]
Aug 27 10:16:21 Ubuntu1804 login[10703]: pam_unix(login:se[…]
Aug 27 10:16:21 Ubuntu1804 systemd-logind[588]: Removed se[…]
^C
$
```
## File-Summarizing Commands
### Counting with `wc`
```
wc [OPTION]... [FILE]...
```
Khi không chọn option nào, lệnh `wc` sẽ hiện ra số dòng, số từ và số byte.
```
[root@hoanganh fuming]# cat random.txt
0.000
hello
VietNam
0101000111
[root@hoanganh fuming]# wc random.txt
 4  4 31 random.txt
```
### Pulling Out Portions with  `cut`
```
cut OPTION... [FILE]...
```
Lệnh `cut` giúp chúng ta có thể hiện ra đoạn thông tin mình cần một cách chính xác
```
$ head -2 /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
$
$ cut -d ":" -f 1,7 /etc/passwd
root:/bin/bash
bin:/sbin/nologin
[…]
$
```
### Discovering Repeated Lines with `uniq`
Hiện thông tin trùng lặp với lệnh `uniq`
```
$ cat NonUniqueLines.txt
A
C
C
A$
$ uniq NonUniqueLines.txt
A C A $
```
### Digesting an MD5 Algorithm
Kiểm tra tính toàn vẹn với `md5sum`
```
[root@hoanganh fuming]# md5sum random.txt
113925936287b254a0e854deb4632ce0  random.txt
```
### Securing Hash Algorithms

SHA(hàm băm) được sử dụng để kiểm tra tính toàn vẹn(integrity) khi chúng được copy hay di chuyển sang vị trí khác
Kiểm tra tên công cụ SHA
```
[root@hoanganh fuming]# ls -l /usr/bin/sha???sum
-rwxr-xr-x. 1 root root 41608 Nov 17  2020 /usr/bin/sha224sum
-rwxr-xr-x. 1 root root 41608 Nov 17  2020 /usr/bin/sha256sum
-rwxr-xr-x. 1 root root 41624 Nov 17  2020 /usr/bin/sha384sum
-rwxr-xr-x. 1 root root 41624 Nov 17  2020 /usr/bin/sha512sum
```
Thử với `sha256` và `sha512`
```
[root@hoanganh fuming]# sha256sum random.txt
5a080d1126cc91a8015d13e846d12d3f130c28e952dcc1dda732faaacb23bb51  random.txt
[root@hoanganh fuming]# sha512sum random.txt
56d6742be977e77849e3e425371748b704547838b83cf42056259715fd5881ab3c7921d656a2fe1483f168eb5023975f38207e6187af82231a64e4361b768313  random.txt
```
# Using Regular Expressions
## Using `grep`
Lệnh `grep` rất mạnh mẽ khi nó dùng    `regular expressions`. Điều này giúp lọc các tệp văn bản.
Syntax
```
grep [OPTION] PATTERN [FILE...]
```
For example:
```
[root@hoanganh fuming]# grep VietNam random.txt
VietNam
```
Dùng thêm option `-f` để tìm các mẫu được lưu trong tệp văn bản
```
$ cat accounts.txt
sshd
Christine
nfsnobody
$
$ fgrep -f accounts.txt /etc/passwd
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
Christine:x:1001:1001::/home/Christine:/bin/bash
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
$
$ grep -F -f accounts.txt /etc/passwd
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
Christine:x:1001:1001::/home/Christine:/bin/bash
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
$
```
## Understanding Basic Regular Expressions
Basic regular expressions (BREs) include characters, such as a dot followed by an asterisk(.*) to represent multiple characters ...
```
$ grep daemon.*nologin /etc/passwd
daemon:x:2:2:daemon:/sbin:/sbin/nologin
[…]
daemon:/dev/null:/sbin/nologin
[…]
$
```
Kí tự `^` cho đầu ra luôn bắt đầu vs pattern
```
$ grep ^root /etc/passwd
root:x:0:0:root:/root:/bin/bash
$
```
Ngược lại kí tự `-v` cha đầu ra không bao gồm pattern.
Ta có thể dùng lớp kí tự để tìm dữ liệu
```
$ cat random.txt
42
Flat Land
Schrodinger's Cat
0010 1010
0000 0010
$
$ grep [[:digit:]] random.txt
42
0010 1010
0000 0010
$
```
## Understanding Extended Regular Expressions
Extend Regular Expressions(EREs) cho nhiều mẫu phức tạp hơn.
For example:
```
$ grep -E "^root|^dbus" /etc/passwd
root:x:0:0:root:/root:/bin/bash
dbus:x:81:81:System message bus:/:/sbin/nologin
$
$
egrep "(daemon|s).*nologin" /etc/passwd
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
[…]
$
```
Có thể thấy kí tự `|` cho đầu ra là một trong 2 mẫu đưa vào. Và `egrep` bằng với `grep -E`
# Using Streams, Redirection, and Pipes
## Redirecting Input and Output
### Handling Standard Input
Lệnh `echo` cho đầu ra văn bản theo STDOUT
```
[root@hoanganh ~]# echo "Hello World"
Hello World
```
STDOUT cho phép bạn chuyển hướng đầu ra bằng toán tử chuyển hướng
```
$ grep nologin$ /etc/passwd
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
[…]
$ grep nologin$ /etc/passwd > NologinAccts.txt
$
$ less NologinAccts.txt
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
[…]
$
```
Để thêm dữ liệu vào tệp có sẵn, ta dùng toán tử `>>`. Nếu tệp chưa tồn tại, nó tự tạo và thêm đầu ra của lệnh vào tệp.
```
$ echo "Nov 16, 2019" > AccountAudit.txt
$
$ wc -l /etc/passwd >> AccountAudit.txt
$
$ cat AccountAudit.txt
Nov 16, 2019
44 /etc/passwd
$
```
### Redirecting Standard Error
Standard Error(STDERR), giống như STDOUT, mặc định gửI đến thiết bị đầu cuối của bạn. Ta có thể dùng toán tử `2>` hoặc `2>>` nếu file đã tồn tại.
```
[root@hoanganh fuming]# ./random.txt 2>> err.txt
[root@hoanganh fuming]# cat err.txt
-bash: ./random.txt: Permission denied
```
### Regular Standard Input
Giống như STDOUT và STDERR, ta có thể chuyển hướng STDIN. Dùng toán tử `<` và lệnh `tr` để thực hiện
```
[root@hoanganh fuming]# cat diem.txt
15 20 30 45 66 77 85 96
[root@hoanganh fuming]# tr " " "," < diem.txt
15,20,30,45,66,77,85,96
```
## Piping Data between Programs
Với pipe(`|`), đầu ra của lệnh trước sẽ là đầu vào của lệnh tiếp theo.
Syntax:
```
Command1 | Command2 | Command3 ...
```
Ví dụ:
```
[root@hoanganh fuming]# grep /bin/bash$ /etc/passwd | wc -l
2
```
Lệnh `tee` cho phép giữ đầu ra trong 1 file và hiện thị với STDOUT
```
$ grep /bin/bash$ /etc/passwd | tee BashUsers.txt
root:x:0:0:root:/root:/bin/bash
user1:x:1000:1000:Student User One:/home/user1:/bin/bash
Christine:x:1001:1001::/home/Christine:/bin/bash
$
$ cat BashUsers.txt
root:x:0:0:root:/root:/bin/bash
user1:x:1000:1000:Student User One:/home/user1:/bin/bash
Christine:x:1001:1001::/home/Christine:/bin/bash
$
```
### Using `sed`
`sed` là một công cụ tuyệt vời giúp người đọc chỉnh sửa nội dung file
Syntax
```
sed [OPTIONS] [SCRIPT]… [FILENAME]
```
Ví dụ
```
$ echo "I like cake." | sed 's/cake/donuts/'
I like donuts.
$
```
Thêm `-g` để thay thế hoàn toàn pattern
```
$ echo "I love cake and more cake." | sed 's/cake/donuts/'
I love donuts and more cake.
$
$ echo "I love cake and more cake." | sed 's/cake/donuts/g'
I love donuts and more donuts.
$
```
Ngoài ra chúng ta có thể xóa 1 từ trong file
```
[root@hoanganh fuming]# cat random.txt
0.000
hello
VietNam
0101000111
Hello
[root@hoanganh fuming]# sed '/Hello/d' random.txt
0.000
hello
VietNam
0101000111
```
`sed` cũng có thể thêm 1 dòng mới tương tự `echo`.
### Generating Command Line
```
$ touch EmptyFile1.txt EmptyFile2.txt EmptyFile3.txt
$
$ ls EmptyFile?.txt
EmptyFile1.txt EmptyFile2.txt EmptyFile3.txt
$
$ ls -1 EmptyFile?.txt | xargs -p /usr/bin/rm
/usr/bin/rm EmptyFile1.txt EmptyFile2.txt EmptyFile3.txt ?...n
$
```
