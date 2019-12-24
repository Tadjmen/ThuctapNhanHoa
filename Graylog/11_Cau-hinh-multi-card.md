# Cấu hình Graylog để đẩy log qua nhiều Card mạng sử dụng Sidecar
Trong trường hợp máy Graylog Server có nhiều card mạng mà ta muốn nhận log từ Toàn bộ các Card mạng đó, trong bài viết này mình sẽ trình bày nội dung cấu hình để có thể nhận Log từ nhiều Card mạng trên máy Graylog Server sử dụng Sidecar

## Cấu hình trên Graylog Server
Đối với Graylog Server đã cấu hình sử dụng Graylog để quản lý log tập trung như đã hướng dẫn tại [Cài đặt Graylog](./02_Cai-dat-graylog.md)

Sửa File cấu hình Graylog Server tại /etc/graylog/server/server.conf
```
vi /etc/graylog/server/server.conf
```
Thay đổi địa chỉ ip của trường `http_bind_address` thành ip `0.0.0.0` như hình sau, mọi cấu hình khác giữ nguyên.

<img src="https://i.imgur.com/rTvTpI2.png">


```
systemctl status graylog-sidecar
```
Như hình là thành công

<img src="https://i.imgur.com/nrfne0I.png">

# Cấu hình sidecar trên server.
## Khai báo input cho sidecar
Trước khi cấu hình sidecar, ta cần khai báo input để graylog server hiểu nó sẽ nhận log từ đâu. Ta thực hiện như sau:

Truy cập vào menu `System` ==> `Inputs`. Sau đó chọn `Beats` và click vào `Launch new input`.
Ở các mục dưới khai báo như sau:
- Node: Chọn tab localhost
- Title: BeatInput
- Bind address: `0.0.0.0` 
- Port: Sửa lại port mà bạn muốn, ở hướng dẫn này tôi chọn 9514. Lưu ý port này sẽ được khai báo ở các bước tiếp theo.
- Các mục còn lại bỏ qua
- Sau đó nhấn `Save`

<img src="https://i.imgur.com/Z8fSWDE.png">

## Cấu hình sidecar trên client.
Kiểm tra Card mạng trên máy Graylog Server

<img src="https://i.imgur.com/avQ2YSl.png">

Quay trở lại máy Client

## Cấu hình sidecar
```
vi /etc/graylog/sidecar/sidecar.yml
```
Dòng server_url khai báo IP của máy graylog server, Client đang đứng trong card mạng nào thì sử dụng IP graylog cùng dải để đẩy log
```
server_url: "http://192.168.182.55:9000/api/"  
```

## Cấu hình sidecar trên server.

Đăng nhập vào graylog server với tài khoản admin.
Truy cập vào `System` ==> `Sidecars`
<img src="https://i.imgur.com/iVqndeJ.png">

Chọn tab `Configuration`

<img src="https://i.imgur.com/1SkaV6V.png">

Chọn tab `Create configuration`

<img src="https://i.imgur.com/XSxhrTy.png">

Khai báo theo thông số như sau.
<img src="https://i.imgur.com/q6KRYnP.png">

Nhấn Create

Mở port với Port vừa cấu hình


```
firewall-cmd --permanent --add-port=9514/udp
firewall-cmd --permanent --add-port=9514/tcp
firewall-cmd --reload
```


Thông số ở File Configuration có thể tùy chỉnh lại cho phù hợp. 

**Lưu ý: Dòng 12 là địa chỉ và cổng vừa config ở bước trước đó**

Quay lại tab `System` ==> `Sidecars` để chọn áp dụng khai báo ở trên, chọn tab `Manage sidecars`

<img src="https://i.imgur.com/wir8k7v.png">

Chọn trường filebeat và áp cấu hình

<img src="https://i.imgur.com/RgShlnE.png">

Chọn `Confirm`

<img src="https://i.imgur.com/ZpW4Trs.png">


# Kiểm tra xem đã hoạt động hay chưa

Đứng trên server mở tab `Search`.
Chúng ta SSH vào máy Client cài sidecar xem có gửi log về sever hay không.

<img src="https://i.imgur.com/ExDizR1.png">

Như vậy chúng ta đã thực hiện thành công cấu hình graylog thu thập log bằng sidecar.
