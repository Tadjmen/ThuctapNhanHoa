# Hướng dẫn cấu hình graylog thu thập log bằng sidecar.

Một số đặc điểm của graylog sidecar như sau:

- Ngoài giao thức `syslog` là một lựa chọn phổ biến để `Graylog Server` thu thập log thì `Graylog Sidecar` cũng là một input được lựa chọn nhiều bởi vì chúng có khả năng quản lý các cấu hình phía client để thu thập log.  
- `Graylog sidecar` có hỗ trợ cả Windows lẫn Linux.
- `Graylog sidecar` là tên gọi trong bản Graylog 3.x trở đi, trước đó nó gọi là `collector sidecar`.  
- `Graylog sidecar` đóng vai trò như một agent để làm nhiệm vụ nhận chỉ thị từ graylog server để thực hiện việc cấu hình việc đẩy log chứ không phải là công cụ đẩy log. Việc đẩy log từ client về server lúc này có thể sử dụng `filebeat` hoặc `winlogbeat`.


## Mô hình triển khai  
<img src="https://i.imgur.com/hkBq0cX.png">

## IP Planning:  
<img src="https://i.imgur.com/dH1uJI2.png">

## Cài đặt
Trên server: CentOS 7 64 bit, Graylog 3.x  
Trên client 1: Kali Linux (192.168.182.151)
Trên client 2: Windows 7 (192.168.182.152)


### Thực hiện update và cài đặt gói bổ trợ.
``` q
apt-get -y update 
apt-get install -y git vim byobu 
```












