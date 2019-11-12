# Hướng dẫn tạo SSH Key bằng MobaXtem
SSH Key bạn cứ hiểu đơn giản là một phương thức chứng thực người dùng truy cập bằng cách đối chiếu giữa một key cá nhân (Private Key) và key công khai(Public Key).
Khi tạo một SSH Key sẽ có cả 2 loại key này. Sau đó ta mang cái public key bỏ lên máy chủ, còn cái private key sẽ lưu ở máy và khi đăng nhập vào server, ta sẽ gửi yêu cầu đăng nhập kèm theo cái Private Key này để gửi tín hiệu đến server, server sẽ kiểm tra xem cái Private key của bạn có khớp với Public key có trên server hay không, nếu có thì bạn sẽ đăng nhập được.
Nội dung giữa Private Key và Public Key hoàn toàn khác nhau, nhưng nó vẫn sẽ nhận diện được với nhau thông qua một thuật toán riêng của nó, đó là so sánh cặp mã hóa.

### Thành phần chính của một SSH Key
- Public Key (dạng file và string) – Bạn sẽ copy ký tự key này sẽ bỏ vào file ~/.ssh/authorized_keys trên server của bạn.
- Private Key (dạng file và string) – Bạn sẽ lưu file này vào máy tính, sau đó sẽ thiết lập cho PuTTY, WinSCP, MobaXterm,..để có thể login.
- Keypharse (dạng string, cần ghi nhớ) – Mật khẩu để mở private key, khi đăng nhập vào server nó sẽ hỏi cái này.
Và một SSH Key có thể sử dụng cho nhiều server khác nhau.

#### Bước 1: Sử dụng lệnh: ssh-keygen -t rsa trên cửa sổ Terminal
<img src="https://i.imgur.com/jjs0IkL.png">
Tiếp tục nó sẽ hỏi bạn có muốn thiết lập keypharse không, nếu muốn thì nhập keypharse cần thiết lập vào rồi Enter.
Sau khi tạo xong, mặc định nó sẽ hiện ra thế này:
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
Và cái public key này (/root/.ssh/id_rsa.pub) bạn sẽ mang lên VPS.

#### Bước 2: Sử dụng SSH-COPY-ID có thể tham khảo tại [đây](https://www.ssh.com/ssh/copy-id)
<img src="https://i.imgur.com/TlCGU0H.png">

#### Bước 3: Sau khi copy thành công mở File authorized_keys ở máy sever lên kiểm tra
tại đây mình đã thêm key trước đó nên có 2 key
<img src="https://i.imgur.com/rFQ1Uv7.png">

#### Bước 4: Sau khi setup thành công thì khi đăng nhập sẽ không cần xác thực lại nữa
<img src="https://i.imgur.com/j851T9l.png">

