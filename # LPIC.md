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
 *For example with   ```echo``` comnand
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

