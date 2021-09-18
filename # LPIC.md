# LPIC
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
 * For example with ```echo``` comnand
 ```
    echo [Option]  [String] ....
 ```
 ## Các siêu kí tự trích dẫn
 * Trong Bash shell có rất nhiều kí tự có ý nghĩa và chức năng đặc biệt. Chúng được gọi là các siêu ký tự trích dẫn(quoting metacharacters).
 ```
    * ? [ ] ' " \ $ ; & ( ) | ^ < >
 ```
 * Ví dụ , kí tự ```$``` biểu thị rằng kí tự này đi cùng với 1 tên biến. Sử dụng lệnh ```echo```, chương trình sẽ cố gắng chạy và hiện thị giá trị của biến.
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
* Chương trình ```Hello.sh``` ở trong thư mục mà nó không nằm trong thư mục của biến môi trường ```PATH```. Do đó khi chạy chương trình trong shell prompt, tin nhắn hiện ra là ```command not found```.