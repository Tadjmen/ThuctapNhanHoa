# Quản lý user trong Unix/Linux
Có 3 kiểu tài khoản trên một hệ thống Unix:\
- Tài khoản gốc (Root account): Là tài khoản Super User có toàn quyền trên hệ thống. Có thể chạy bất cứ lệnh nào mong muốn
- Các tài khoản hệ thống: Các tài khoản hệ thống được tạo sẵn để phục vụ các hoạt động riêng rẽ trên hệ thống, sửa đổi thông tin các User này có thể gây ra lỗi đối với toàn hệ thống.
- Các tài khoản người dùng cá nhân: Tài khoản này được cung cấp những tính năng mang tính tương đối trong hệ thống, bị giới hạn truy cập vào những vùng quan trọng.

## Các tài khoản người dùng cá nhân
Có 4 file chính quản lý người sử dụng:
1. `/etc/passwd`: Giữ tài khoản người dùng và thông tin mật khẩu. File này giữ các thông tin quan trọng về các tài khoản trên hệ thống Unix.
2. `/etc/shadow`: Giữ mật khẩu được biên thành mật mã của tài khoản tương ứng. Không phải tất cả các hệ thống đều hỗ trợ file này.
3. `/etc/group`: File này giữ thông tin nhóm cho mỗi tài khoản.
4. `/etc/gshadow`: File này giữ các thông tin tài khoản nhóm bảo mật.
Chúng ta có thể dùng lệnh `Cat` để kiểm tra những File này.

## Các lệnh trong Linux để quản lý các tài khoản cá nhân và nhóm.
|Lệnh|Miêu tả|
|---|---|
|useradd|Thêm một User mới|
|usermod|Chỉnh sửa thuộc tính tài khoản|
|userdel|Xóa tài khoản|
|groupadd|Thêm tài khoản Group mới|
|groupmod|Chỉnh sửa thuộc tính Group|
|groupdel|Xóa tài khoản Group|

## Tạo một nhóm trong Linux
Cú pháp tạo nhóm mới trong Linux\
`groupadd [-g gid] groupname`\
Các tham số
|Tùy chọn|Miêu tả|
|---|---|
|-g GID|Giá trị ID|
|groupname|Tên Group|

Tạo nhóm Dev2 `groupadd dev2`\
## Chỉnh sửa một nhóm trong Unix/Linux
Để thay đổi tên nhóm dev2 thành dev, bạn gõ như sau:\
`groupmod -n dev dev2`
Đổi ID Group
`groupmod -g 444 dev`\

Kiểm tra xem nhóm đã được tạo thành công hay chưa\

<pre>[root@localhost etc]# cat group
root:x:0:
bin:x:1:
daemon:x:2:
sys:x:3:
adm:x:4:
tty:x:5:
disk:x:6:
lp:x:7:
mem:x:8:
kmem:x:9:
wheel:x:10:
cdrom:x:11:
mail:x:12:postfix
man:x:15:
dialout:x:18:
floppy:x:19:
games:x:20:
tape:x:33:
video:x:39:
ftp:x:50:
lock:x:54:
audio:x:63:
nobody:x:99:
users:x:100:
utmp:x:22:
utempter:x:35:
input:x:999:
systemd-journal:x:190:
systemd-network:x:192:
dbus:x:81:
polkitd:x:998:
libstoragemgmt:x:997:
ssh_keys:x:996:
abrt:x:173:
rpc:x:32:
apache:x:48:
sshd:x:74:
slocate:x:21:
postdrop:x:90:
postfix:x:89:
chrony:x:995:
ntp:x:38:
tcpdump:x:72:
stapusr:x:156:
stapsys:x:157:
stapdev:x:158:
**dev:x:444:**
[root@localhost etc]#

</pre>

## Xóa một nhóm trong Unix/Linux
`groupdel dev`\
Lệnh này chỉ gỡ bỏ nhóm, không phải bất kỳ file nào liên quan tới nhóm. Nên những File của nhóm vẫn còn trong thư mục home
