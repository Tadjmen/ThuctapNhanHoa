# Các EventID quan trọng đối với Remote Desktop
Các Sự kiện trên Linux được ghi lại vào File log, còn đối với windows sẽ được ghi vào Event View theo các Name cụ thể ứng với từng log.

Trong bài viết này chúng ta sẽ list ra các trường hợp khi Remote Desktop tới máy chủ Windows

Để mở Event viewer ta bấm tổ hợp phím `Windows+R` sau đó nhập `eventvwr`
<img src="https://i.imgur.com/UjofXA0.png">

## Khi Remote Desktop đúng User đúng Password
Kiểm tra tại `Event viewer` > `Windows Logs` > `Security`

Sẽ thấy xuất hiện Event ID 4624 được định nghĩa là Event ID sẽ được sinh ra khi có một kết nối Remote Desktop thành công vào máy chủ.

<img src="https://i.imgur.com/dRqiars.png">

tại đây ta có thể thấy được những thông tin sau:
- Event ID: 4624
- Log Name: Security
- phần bản tin: An account was successfully logged on.
- logged: 12/24/2019 4:35:34 PM
- level: Infomation
- Computer: Tên máy tính được đăng nhập

Trong đó:
- Event ID: là ID sự kiện
- Log Name: Tên bản tin log
- phần bản tin: là bản tin log
- logged: thời gian xuất hiện sự kiện
- level: mức độ cảnh báo
- Computer: Tên máy tính được đăng nhập

## Khi Remote Đúng User sai Password
Kiểm tra tại `Event viewer` > `Windows Logs` > `Security`

Sẽ thấy xuất hiện Event ID 4625 được định nghĩa là Event ID sẽ được sinh ra khi có một kết nối Remote Desktop thất bại vào máy chủ.

<img src="https://i.imgur.com/WUveSqq.png">


tại đây ta có thể thấy được những thông tin sau:
- Event ID: 4625
- Log Name: Security
- phần bản tin: An account failed to log on.
- logged: 12/24/2019 4:54:50 PM
- level: Infomation
- Computer: Tên máy tính được đăng nhập

Trong đó:
- Event ID: là ID sự kiện
- Log Name: Tên bản tin log
- phần bản tin: là bản tin log
- logged: thời gian xuất hiện sự kiện
- level: mức độ cảnh báo
- Computer: Tên máy tính được đăng nhập

<img src="https://i.imgur.com/znU7iYd.png">

## Khi Remote sai User
Kiểm tra tại `Event viewer` > `Windows Logs` > `Security`

Sẽ thấy xuất hiện Event ID 4625 được định nghĩa là Event ID sẽ được sinh ra khi có một kết nối Remote Desktop thất bại vào máy chủ.

<img src="https://i.imgur.com/omEBq6a.png">


tại đây ta có thể thấy được những thông tin sau:
- Event ID: 4625
- Log Name: Security
- Account Name: sdsdsdsds
- phần bản tin: An account failed to log on.
- logged: 12/24/2019 4:54:50 PM
- level: Infomation
- Computer: Tên máy tính được đăng nhập

Trong đó:
- Event ID: là ID sự kiện
- Log Name: Tên bản tin log
- Account Name: Tên user
- phần bản tin: là bản tin log
- logged: thời gian xuất hiện sự kiện
- level: mức độ cảnh báo
- Computer: Tên máy tính được đăng nhập
*Chú ý*: *Có thêm phần Account Name*

## Remote sai User hoặc Password
Kiểm tra tại `Event viewer` > `Applications and Services Logs` > `Microsoft` > `Windows` > `RemoteDesktopServices-RdpCoreTS` > `Operational`

Nhấn vào `Filter Current log...`
<img src="https://i.imgur.com/MZTf7qD.png">

Tìm EventID 140

<img src="https://i.imgur.com/HOxoEvP.png">

Sẽ chỉ thấy xuất hiện Event ID 140 được định nghĩa là Event ID sẽ được sinh ra khi có một kết nối Remote Desktop thất bại vào máy chủ.

tại đây ta có thể thấy được những thông tin sau:
- Event ID: 140
- Log Name: Microsoft-Windows-RemoteDesktopServices-RdpCoreTS/Operational
- Account Name: Administrator
- phần bản tin: A connection from the client computer with an IP address of 192.168.182.1 failed because the user name or password is not correct.
- logged: 12/24/2019 5:02:36 PM
- level: Warning
- Computer: Tên máy tính được đăng nhập


Trong đó:
- Event ID: là ID sự kiện
- Log Name: Tên bản tin log
- Account Name: Tên user
- phần bản tin: Có một kết nối từ IP **x** kết nối tới nhưng nhập sai User hoặc mật khẩu
- logged: thời gian xuất hiện sự kiện
- level: mức độ cảnh báo
- Computer: Tên máy tính được đăng nhập

Lưu ý: trên phần bản tin Log có ghi lại IP đã thực hiện Remote Desktop sai vào máy chủ, từ đây có thể trích xuất thông tin để xử lý, phần khoanh đỏ là phần IP Remote thất bại

<img src="https://i.imgur.com/tEiLfsu.png">