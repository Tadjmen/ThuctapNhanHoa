# Log là gì?
Log ghi lại liên tục các thông báo về hoạt động của cả hệ thống hoặc của các dịch vụ được triển khai trên hệ thống và file tương ứng. Log file thường là các file văn bản thông thường dưới dạng “clear text” tức là bạn có thể dễ dàng đọc được nó, vì thế có thể sử dụng các trình soạn thảo văn bản (vi, vim, nano…) hoặc các trình xem văn bản thông thường (cat, tailf, head…) là có thể xem được file log.

Các file log có thể nói cho bạn bất cứ thứ gì bạn cần biết, để giải quyết các rắc rối mà bạn gặp phải miễn là bạn biết ứng dụng nào. Mỗi ứng dụng được cài đặt trên hệ thống có cơ chế tạo log file riêng của mình để bất cứ khi nào bạn cần thông tin cụ thể thì các log file là nơi tốt nhất để tìm.

Các tập tin log được đặt trong thư mục `/var/log`. Bất kỳ ứng dụng khác mà sau này bạn có thể cài đặt trên hệ thống của bạn có thể sẽ tạo tập tin log của chúng tại `/var/log`. Dùng lệnh `ls -l /var/log` để xem nội dung của thư mục này.

## VD: Ý nghĩa một số file log thông dụng có mặc định trên /var/log

`/var/log/messages` – Chứa dữ liệu log của thông báo hệ thống nói chung, bao gồm cả các thông báo trong quá trình khởi động hệ thống.  
`/var/log/cron` – Chứa dữ liệu log của cron deamon. Bắt đầu và dừng cron cũng như cronjob thất bại.  
`/var/log/maillog` hoặc `/var/log/mail.log` – Thông tin log từ các máy chủ mail.  
`/var/log/wtmp` – Chứa lịch sử đăng nhập và đăng xuất .  
`/var/log/btmp` – Thông tin đăng nhập không thành công  
`/var/run/utmp` – Thông tin log trạng thái đăng nhập hiện tại của mỗi người dùng.  
`/var/log/dmesg` – Thư mục này có chứa thông điệp rất quan trọng về kernel ring buffer. Lệnh dmesg có thể được sử dụng để xem các tin nhắn của tập tin này.  
`/var/log/secure` – Thông điệp liên quan đến bảo mật sẽ được lưu trữ ở đây. Điều này bao gồm thông điệp từ SSH daemon, mật khẩu thất bại, người dùng không tồn tại, vv.  

## Các lệnh thường dùng khi thao tác với Log

|Lệnh|Tác Dụng|
|---|---|
|tail|Xem nội dung cuối File|
|tailf|Xem nội dung cuối liên tục File log đến khi dừng|
|grep|Tìm chuỗi|
|egrep|Sử dụng grep để tìm 2 từ khác nhau : egrep -w 'word1\|word2' /pack to file|
|ack|Tìm chuỗi|
|cat|Đọc nội dung File|
|head|Đọc nội dung đầu File|
|find|Tìm chuỗi|
|ls|Liệt kê File, thư mục trong Foder đang đứng|
|history|Lịch sử lệnh|


## Một số log thường gặp

**Log SSH**: `/var/log/secure`
```
[root@localhost ~]# cat /var/log/secure |grep ssh | tail
Nov 30 01:07:26 localhost sshd[1300]: Failed password for invalid user r\303\264t from 192.168.182.1 port 51256 ssh2
Nov 30 01:07:27 localhost sshd[1300]: Failed password for invalid user r\303\264t from 192.168.182.1 port 51256 ssh2
Nov 30 01:07:27 localhost sshd[1300]: error: maximum authentication attempts exceeded for invalid user r\\303\\264t from 192.168.182.1 port 51256 ssh2 [preauth]
Nov 30 01:07:27 localhost sshd[1300]: Disconnecting: Too many authentication failures [preauth]
Nov 30 01:07:27 localhost sshd[1300]: PAM 3 more authentication failures; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.182.1
Nov 30 01:07:27 localhost sshd[1300]: PAM service(sshd) ignoring max retries; 4 > 3
Nov 30 01:07:37 localhost sshd[1305]: Accepted password for root from 192.168.182.1 port 51257 ssh2
Nov 30 01:07:37 localhost sshd[1309]: Accepted password for root from 192.168.182.1 port 51258 ssh2
Nov 30 01:07:37 localhost sshd[1305]: pam_unix(sshd:session): session opened for user root by (uid=0)
Nov 30 01:07:38 localhost sshd[1309]: pam_unix(sshd:session): session opened for user root by (uid=0)
[root@localhost ~]#
```

**Log ghi lại những lần đăng nhập thành công**: `last -f /var/log/wtmp`
```
[root@localhost ~]# last -f /var/log/wtmp
root     pts/0        192.168.182.1    Sat Nov 30 01:07   still logged in
reboot   system boot  3.10.0-1062.el7. Sat Nov 30 01:06 - 01:19  (00:12)

wtmp begins Sat Nov 30 01:06:53 2019
[root@localhost ~]#
```

**Log ghi lại những lần đăng nhập thất bại**:  `lastb -f /var/log/btmp`
```
[root@localhost ~]# lastb -f /var/log/btmp
r**t     ssh:notty    192.168.182.1    Sat Nov 30 01:07 - 01:07  (00:00)
r**t     ssh:notty    192.168.182.1    Sat Nov 30 01:07 - 01:07  (00:00)
r**t     ssh:notty    192.168.182.1    Sat Nov 30 01:07 - 01:07  (00:00)
r**t     ssh:notty    192.168.182.1    Sat Nov 30 01:07 - 01:07  (00:00)
r**t     ssh:notty    192.168.182.1    Sat Nov 30 01:07 - 01:07  (00:00)
r**t     ssh:notty    192.168.182.1    Sat Nov 30 01:07 - 01:07  (00:00)

btmp begins Sat Nov 30 01:07:13 2019
[root@localhost ~]#
```

**Access Log Apache**: `tailf /var/log/httpd/access_log`
```
[root@localhost html]# tailf /var/log/httpd/access_log
192.168.182.1 - - [30/Nov/2019:07:31:07 +0700] "GET /index.php?=PHPE9568F34-D428-11d2-A769-00AA001ACF42 HTTP/1.1" 200 2524 "http://192.168.182.128/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
192.168.182.1 - - [30/Nov/2019:07:31:07 +0700] "GET / HTTP/1.1" 200 43730 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
192.168.182.1 - - [30/Nov/2019:07:31:07 +0700] "GET /index.php?=PHPE9568F35-D428-11d2-A769-00AA001ACF42 HTTP/1.1" 200 2146 "http://192.168.182.128/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
```

**Error Log Apache** : `/var/log/httpd/tailf error_log`
```
[root@localhost httpd]#  tailf /var/log/httpd/error_log
[Sat Nov 30 07:22:35.506674 2019] [:error] [pid 1964] [client 192.168.182.1:53303] PHP Warning:  phpinfo(): It is not safe to rely on the system's timezone settings. You are *required* to use the date.timezone setting or the date_default_timezone_set() function. In case you used any of those methods and you are still getting this warning, you most likely misspelled the timezone identifier. We selected the timezone 'UTC' for now, but please set date.timezone to select your timezone. in /var/www/html/index.php on line 1
[Sat Nov 30 07:22:35.678214 2019] [:error] [pid 1964] [client 192.168.182.1:53303] PHP Warning:  phpinfo(): It is not safe to rely on the system's timezone settings. You are *required* to use the date.timezone setting or the date_default_timezone_set() function. In case you used any of those methods and you are still getting this warning, you most likely misspelled the timezone identifier. We selected the timezone 'UTC' for now, but please set date.timezone to select your timezone. in /var/www/html/index.php on line 1
```

# Tổng quan Syslog

