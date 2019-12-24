# Cài đặt và cấu hình DNS Server
## DNS Server là gì
Mỗi Website có một tên (là tên miền hay đường dẫn URL:Universal Resource Locator) và một địa chỉ IP. Địa chỉ IP gồm 4 nhóm số cách nhau bằng dấu chấm(Ipv4). Khi mở một trình duyệt Web và nhập tên website, trình duyệt sẽ đến thẳng website mà không cần phải thông qua việc nhập địa chỉ IP của trang web. Quá trình “dịch” tên miền thành địa chỉ IP để cho trình duyệt hiểu và truy cập được vào website là công việc của một DNS server. Các ﻿DNS trợ giúp qua lại với nhau để dịch địa chỉ “IP” thành “tên” và ngược lại. Người sử dụng chỉ cần nhớ “tên”, không cần phải nhớ địa chỉ IP (địa chỉ IP là những con số rất khó nhớ).DNS sử dụng cổng port 53 để truyền thông tin .Đây chính là chức năng chính của một con DNS Server trong việc hỗ trợ phân giải tên miền 1 cách đơn giản , giúp người dùng đầu cuối dễ dàng nhập các địa chỉ web , địa chỉ Local mà không gặp rắc rối .

## Các khái niệm trong DNS 
### Primary DNS Server (PDS)
Primary DNS Server (PDS) là nguồn xác thực thông tin chính thức cho các tên miền mà nó được phép quản lý. Thông tin về một tên miền do PDS ﻿được phân cấp quản lý thì được lưu trữ tại đây và sau đó có thể được chuyển sang các Secondary DNS Server (SDS).

Các tên miền do PDS quản lý thì được tạo, và sửa đổi tại PDS và sau đó được cập nhật đến các SDS .
### Secondary DNS Server (SDS)
DNS được khuyến nghị nên sử dụng ít nhất là hai DNS server để lưu địa chỉ cho mỗi một vùng (zone). PDS quản lý các vùng và SDS được sử dụng để lưu trữ dự phòng cho vùng, và cho cả PDS. SDS không nhất thiết phải có nhưng khuyến khích hãy sử dụng . SDS được phép quản lý tên miền nhưng dữ liệu về tên miền không phải được tạo ra từ SDS mà được lấy về từ PDS.

SDS có thể cung cấp các hoạt động ở chế độ không tải trên mạng. Khi lượng truy vấn vùng (zone) tăng cao, PDS sẽ chuyển bớt tải sang SDS (quá trình này còn được gọi là cân bằng tải), hoặc khi PDS bị sự cố thì SDS hoạt động thay thế cho đến khi PDS hoạt động trở lại .

### Các khái niệm trong Zone
- primary zone: cho phép đọc và ghi cơ sở dữ liệu và có toàn quyền trong việc update dữ liệu của DNS
- secondary zone: cho phép đọc và ghi bản sao của sơ sở dữ liệu và muốn được cập nhật zone thì phải đồng bộ với Primary zone
- forwarder: là kỹ thuật cho phép name server nội bộ gửi yêu cầu truy vấn đến server khác để phân giải những tên miền bên ngoài hệ thống
- Delegation (sự ủy quyền) : 1 miền có thể tổ chức thành miền con, mỗi miền con có thể ủy quyền cho 1 tổ chức khác, và tổ chức này phải chịu trách nhiệm duy trì thông tin trong miền này

