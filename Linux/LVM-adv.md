# LVM ADV
Hiển thị danh sách các Hard Drives trên hệ thống bằng câu lệnh `lsblk`

```
[root@centos_client ~]# lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda               8:0    0   15G  0 disk
├─sda1            8:1    0    1G  0 part /boot
└─sda2            8:2    0   14G  0 part
  ├─centos-root 253:0    0 12.5G  0 lvm  /
  └─centos-swap 253:1    0  1.5G  0 lvm  [SWAP]
sdb               8:16   0    5G  0 disk
sdc               8:32   0    5G  0 disk
├─sdc1            8:33   0    3G  0 part
└─sdc2            8:34   0    1G  0 part
sr0              11:0    1  4.4G  0 rom
[root@centos_client ~]#
```

Tạo Partition

`fdisk /dev/sdc`

Trong đó bạn chọn `n` để bắt đầu tạo partition
Bạn chọn `p` để tạo partition primary
Bạn chọn `1` để tạo partition primary 1
Tại `First sector (2048-20971519, default 2048)` bạn để mặc định
Tại `Last sector, +sectors or +size{K,M,G} (2048-20971519, default 20971519)` bạn chọn `+1G` để partition bạn tạo ra có dung lượng 1 G
Bạn chọn `w` để lưu lại và thoát.
Tiếp theo bạn thay đổi định dạng của partition vừa mới tạo thành LVM



Bạn chọn `t` để thay đổi định dạng partition
Bạn chọn `8e` để đổi thành LVM
Tương tự, bạn tạo thêm các partition primary từ sdb


Create a LVM layout