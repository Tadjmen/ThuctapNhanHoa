# Swap memory trong Linux
Swap Memory được sử dụng khi hệ thống của bạn quyết định rằng nó cần thêm bộ nhớ RAM cho quá trình hoạt động và bộ nhớ RAM hiện tại không còn đủ để sử dụng. Nếu điều đó xãy ra, các tài nguyên và dữ liệu tạm thời không hoạt động trên bộ nhớ RAM sẽ được di chuyển để lưu trữ vào không gian Swap để giải phóng bộ nhớ RAM và sử dụng cho việc khác.

Lưu ý rằng thời gian truy cập vào vùng Swap là chậm hơn rất nhiều, do đó bạn không nên coi việc sử dụng Swap là một phương pháp thay thế cho (RAM).

Linux Swap có hai dạng: phân vùng & File. Để xem nó nằm ở đâu, hãy sử dụng lệnh `swapon` .

```[root@localhost /]# swapon -s
Filename                                Type            Size    Used    Priority
/dev/dm-1                               partition       2097148 0       -2
[root@localhost /]#
```