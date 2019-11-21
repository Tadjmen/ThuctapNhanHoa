# Bash shell programming
Dòng đầu tiên của tập lệnh, bắt đầu bằng `#!/bin/bash` chứa đường dẫn đầy đủ của trình thông dịch sẽ được sử dụng trên tệp. Trình thông dịch được giao nhiệm vụ thực thi các câu lệnh tuân theo nó trong kịch bản lệnh. Thông dịch viên thường sử dụng bao gồm:
```
/usr/bin/perl
/bin/bash
/bin/csh
/bin/tcsh
/bin/ksh
/usr/bin/python
/bin/sh
```
Bash shell có thể tương tác qua lại như sau
```
[root@centos_client ~]# cat 1
#!/bin/bash
   # Interactive reading of variables
   echo "Nhap ten cua ban"
   read sname
   # Display of variable values
   echo "Xin chao "$sname"!"
[root@centos_client ~]# ./1
Nhap ten cua ban
Trung
Xin chao Trung!
[root@centos_client ~]#
```

```
[root@centos_client ~]# cat $?
#!/bin/bash
   # Interactive reading of variables
   echo "Nhap ten cua ban"
   read sname
   # Display of variable values
   echo "Xin chao "$sname"!"
```

## Cú pháp cơ bản

|Kí tự|Mô tả|
|---|---|
|#|Được sử dụng để thêm nhận xét, trừ khi được sử dụng dưới dạng # hoặc #! khi bắt đầu một kịch bản|
|||Được sử dụng ở cuối dòng để biểu thị tiếp tục cho dòng tiếp theo|
|;|Được sử dụng để giải thích những gì sau một lệnh mới|
|$|Chỉ ra cái gì sau đây là một biến|