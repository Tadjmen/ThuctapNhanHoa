# Filtering data trong SQL
## WHERE 
WHERE cho phép bạn chỉ định một điều kiện tìm kiếm cho các hàng được trả về bởi một truy vấn.  
Cú pháp:
```
SELECT 
    select_list
FROM
    table_name
WHERE
    search_condition;
```
`Search_condition` là sự kết hợp của một hoặc nhiều vị từ bằng cách sử dụng toán tử logic AND, OR và NOT.  
Trong MySQL, một vị từ là một biểu thức Boolean đánh giá thành `TRUE`, `FALSE` hoặc `UNKNOWN`.  
Bất kỳ hàng nào từ tên_bảng khiến `search_condition` đánh giá thành TRUE sẽ được list ra trong tập kết quả cuối cùng.






















    