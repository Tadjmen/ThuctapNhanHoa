# MySQL Data Types
## 

<img src=https://i.imgur.com/hqXeKjd.png>

## MySQL numeric data types
Kiểu số

Bảng sau đây cho thấy tóm tắt về các loại dữ liệu số trong MySQL:

|Numeric Types	|Description|
|---|---|
| TINYINT|	A very small integer|
| SMALLINT|	A small integer|
| MEDIUMINT|	A medium-sized integer|
| INT|	A standard integer|
| BIGINT|	A large integer|
| DECIMAL|	A fixed-point number|
| FLOAT	|A single-precision floating point |number|
| DOUBLE|	A double-precision floating point number|
| BIT|	A bit field|

## MySQL Boolean data type
Kiểu Boolean
MySQL không có kiểu dữ liệu BOOLESBoolean tích hợp
## MySQL String data types

|String Types|	Description|
|---|---|
| CHAR	A fixed-length nonbinary (character) string|
| VARCHAR|	A variable-length non-binary string|
| BINARY|	A fixed-length binary string|
| VARBINARY	|A variable-length binary string|
| TINYBLOB|	A very small BLOB (binary large object)|
| BLOB|	A small BLOB
| MEDIUMBLOB|	A medium-sized BLOB|
| LONGBLOB|	A large BLOB
| TINYTEXT|	A very small non-binary string|
| TEXT|	A small non-binary string|
| MEDIUMTEXT|	A medium-sized non-binary string|
| LONGTEXT|	A large non-binary string|
| ENUM|	An enumeration; each column value may be assigned one enumeration member|
| SET|	A set; each column value may be assigned zero or more SET members|

## MySQL date and time data types
Kiểu date time

|Date and Time Types|	Description|
|---|---|
|| DATE	|A date value in CCYY-MM-DD format|
| TIME|	A time value in hh:mm:ss format|
| DATETIME	|A date and time value inCCYY-MM-DD hh:mm:ssformat|
| TIMESTAMP	|A timestamp value in CCYY-MM-DD hh:mm:ss format|
| YEAR|	A year value in CCYY or YY format|

### MySQL INT Data Type
<img src=https://i.imgur.com/aiS6EAi.png>

### MySQL INT with the ZEROFILL attribute
Tạo bảng:  
```
CREATE TABLE zerofill_tests(
    id INT AUTO_INCREMENT PRIMARY KEY,
    v1 INT(2) ZEROFILL,
    v2 INT(3) ZEROFILL,
    v3 INT(5) ZEROFILL
);
```

CHèn dữ liệu vào
```
INSERT INTO zerofill_tests(v1,v2,v3)
VALUES(1,6,9);
```

 query data

```
SELECT 
    v1, v2, v3
FROM
    zerofill_tests;
```

Kết quả: 

<img src=https://sp.mysqltutorial.org/wp-content/uploads/2015/11/MySQL-INT-with-ZEROFILL.jpg>

## MySQL DECIMAL Data Type
Khai 























