# Các EventID quan trọng đối với Windows
Các Sự kiện trên Linux được ghi lại vào File log, còn đối với windows sẽ được ghi vào Event View theo các Name cụ thể ứng với từng log.

Đối với log về Đăng nhập và Remote Desktop sẽ có những log đáng chú ý sau:

## Log về Security
Name: **Security**
- **EventID 4625**: An account failed to log on.: Đăng nhập sai
- **EventID 4624**: An account was successfully logged on.: Đăng nhập thành công
- **EventID 4634**: An account was logged off.: Một tài khoản đã Logoff
 
## Log về Remote Desktop 
Name: **Microsoft-Windows-TerminalServices-LocalSessionManager/Operational** 

và

 **Microsoft-Windows-TerminalServices-RemoteConnectionManager/Operational**
- **EventID 1149**: (Remote Desktop Services: User authentication succeeded: Một người mới Remote Desktop thành công. 	
- **EventID 23**:  Remote Desktop Services: Session logoff succeeded.: Một phiên đăng nhập tiến vào trạng thái Logoff
- **EventID 24**: (Remote Desktop Services: Session has been disconnected : Nhấn cắt cửa sổ Đisconnect
- **EventID 25**: (Remote Desktop Services: Session reconnection succeeded): Người từng Remote rồi remote lại, có nghĩa là Reconnect lại phiên cũ
 
- **EventID 39**: (Session \<A> has been disconnected by session \<B>) Disconnect phiên
 
- **EventID 40**: (Session \<A> has been disconnected, reason code \<B>) Disconnect, lý do bên dưới:
    - reason code 0 (No additional informationis available): Không có thông tin gì thêm
    - reason code 5 (The client’s connectionwas replaced by another connection) : Cókết nối Remote mới
    - reason code 11 (User activity has initiatedthe disconnect): Người dùng truy cập vào =>phiên bị dis

## Log về Remote Desktop bổ sung
Name: **Microsoft-Windows-RemoteDesktopServices-RdpCoreTS/Operational**		

- **EventID 140**: Remote Desktop sai user hoặc password
		
		
		