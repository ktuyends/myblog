---
title: "SQL Notes - Tổng hợp cú pháp SQL"
subtitle: ""
slug: basic-sql
date: 2022-05-12
lastmod: 2022-05-12
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["SQL", "SQL for DA"]
categories: []
series: [SQL for Data Analysis]
series_weight: 2
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
{{< figure src="./sql-commands.png" >}}

## 1. Data Definition Language

DDL ta có thể hiểu đơn giản là các câu lệnh giúp chúng ta tạo, sửa đổi hoặc xóa các đối tượng CSDL như databases, tables, views, functions...

### 1.1. CREATE TABLE

Cú pháp:

```sql
-- Tạo bảng
CREATE TABLE table_name(
  column_name constraints,
  CONSTRAINT 
);

-- Ví dụ
CREATE TABLE IF NOT EXISTS STAFF
(
    STAFF_ID         VARCHAR(20)
  , STAFF_TYPE       VARCHAR(30)
  , SCHOOL_ID        VARCHAR(20)
  , FIRST_NAME       VARCHAR(100) NOT NULL
  , LAST_NAME        VARCHAR(100) NOT NULL
  , AGE              INT
  , DOB              DATE
  , GENDER           VARCHAR(10) CHECK (GENDER IN ('M', 'F', 'Male', 'Female'))
  , JOIN_DATE        DATE
  , ADDRESS_ID       VARCHAR(20)
  , CONSTRAINT PK_STAFF PRIMARY KEY(STAFF_ID)
  , CONSTRAINT FK_STAFF_SCHL FOREIGN KEY(SCHOOL_ID) REFERENCES SCHOOL(SCHOOL_ID)
  , CONSTRAINT FK_STAFF_ADDR FOREIGN KEY(ADDRESS_ID) REFERENCES ADDRESS(ADDRESS_ID)
);
```

### 1.2. Data Type

Một số kiểu dữ liệu phổ biến:

- **VARCHAR**: Kiểu ký tự bao gồm các ký tự alphabets, numbers, alphanumeric và một số ký tự đặc biệt.
- **INT**: Kiểu dữ liệu số nguyên.
- **FLOAT**: Kiểu dữ liệu số thực.
- **DATE**: Kiểu ngày tháng năm.
- **BOOLEAN**: Kiểu dữ liệu chỉ có hai giá trị _(TRUE = 1, FALSE = 0)_.

### 1.3. Constraints

Constraints là các ràng buộc áp dụng cho các giá trị trong một cột. Hiểu nôm na là các giá trị khi nhập vào phải thỏa mãn một hoặc một số điều kiện nào đó. Một số constraints phổ biến:

- **CHECK**: Cho phép kiểm soát các giá trị được nhập vào một cột.
- **NOT NULL**: Cột không được có giá trị Null.
- **UNIQUE**: Các giá trị trong cột là duy nhất, không được phép lặp lại.
- **PRIMARY KEY**: Chỉ định cột khóa chính. Cột khóa chính là cột _(NOT NULL & UNIQUE)_.
- **FOREIGN KEY**: Chỉ định cột khóa ngoại, đây là cột xác định mối quan hệ giữa các bảng với nhau.

### 1.4. ALTER

ALTER thường được sử dụng để sửa cấu trúc của các Table hiện có:

```sql
ALTER TABLE <Table_Name> DROP COLUMN <Column_Name>; -- Drop a column.
ALTER TABLE <Table_Name> ADD COLUMN <Column_Name> VARCHAR(100); -- Add new column.
ALTER TABLE <Table_Name> ALTER COLUMN <Column_Name> TYPE VARCHAR(1); -- Change data type of a column.
ALTER TABLE <Table_Name> RENAME COLUMN <Column_Name> TO <New_Column_Name>; -- Rename a column.
ALTER TABLE <Table_Name> ADD CONSTRAINT <Constraint_Name> UNIQUE (<Column_Name>); -- Add new constraint
ALTER TABLE <Table_Name> DROP CONSTRAINT <Constraint_Name>; -- Drop a constraint.
ALTER TABLE <Table_Name> RENAME TO <New_Table_Name>; -- Rename a table.
```

### 1.5. DELETE, TRUNCATE, DROP

Về cơ bản 3 lệnh này được sử dụng để xóa dữ liệu, trong đó:

- **DELETE**: Xóa các dòng trong bảng theo một điều kiện nào đó. Dữ liệu có thể phục hồi.
- **TRUNCATE**: Xóa tất cả các dòng trong bảng khỏi bộ nhớ, không thể phục hồi lại.
- **DROP**: Xóa một bảng khỏi database.

```sql
-- DELETE
DELETE FROM ten_bang; -- Xóa bảng

-- TRUNCATE
TRUNCATE TABLE ten_bang

-- DROP
DROP TABLE ten_bang;
```

## 2. Data Manipulation Language

DML được sử dụng để nhập, sửa hoặc xóa dữ liệu từ databases. Nghĩ theo một hướng khác, thì DDL được sử dụng để tương tác với _Tables_ và _Columns_, còn DML thì được sử dụng để tương tác với các _Record_.

### 2.1. INSERT

Câu lệnh INSERT dùng để nhập dữ liệu vào Tables:

```sql
-- Nhập dữ liệu cơ bản
INSERT INTO table_name (column_list)
VALUES
    (value_list_1),
    (value_list_2),
    ...
    (value_list_n);

-- Nhập dữ liệu từ câu lệnh Select
INSERT INTO table_name (column1, column2, … )
SELECT expression_1, expression_2, …
FROM source_tables
WHERE conditions;
```

### 2.2. UPDATE

Câu lệnh UPDATE dùng để sửa dữ liệu trong Tables:

```sql
-- Sửa một giá trị trong các cột 
UPDATE table_name
SET column_name_1 = new_value, column_name_2 = new_value
WHERE <conditional>
```

### 2.3. DELETE

DELETE dùng để xóa các hàng dữ liệu thỏa mãn một điều kiện nào đó.

```sql
-- xóa các hàng dữ liệu
DELETE FROM table_name WHERE conditional;
```


## 3. Câu lệnh SELECT

### 3.1. Cú pháp cơ bản

```sql
-- Cú pháp cơ bản
SELECT <column_name> [AS new_name]  -- Lấy ra các cột, SELECT DISTINCT, SELECT TOP
FROM <table_name>                   -- Từ một bảng nào đó
WHERE <conditional>                 -- Sau đó lọc ra các record thỏa mãn điều kiện nào đó
ORDER BY <column_name> [DESC];      -- Sắp xếp các giá trị tăng dần

-- Mở rộng với GROUP BY và HAVING
SELECT <column_name>     -- Lấy ra các cột
FROM <table_name>        -- Từ một bảng nào đó
WHERE <conditional>      -- Sau đó lọc ra các record thỏa mãn điều kiện nào đó
GROUP BY <column_name>   -- Gom nhóm
HAVING <agregate_filter> -- Hàm lọc các nhóm thỏa mãn điều kiện nào đó
ORDER BY <column_name>   -- Sắp xếp các giá trị tăng dần, DESC giảm dần
LIMIT n;                 -- Lấy ra n bản ghi đầu tiên, trong SQL Server là SELECT TOP n  
```

Thứ tự thực hiện các câu lệnh trong SQL:

{{< figure src="./sql-query-order.png" width=60% >}}

### 3.2. Toán tử

- Các toán tử cơ bản: _+, -, *, /, % (chia lấy phần dư)_
- Các toán tử so sánh: _=, !=, <, <=, >, >=_
- Các toán tử logic: _AND, OR, NOT, BETWEEN...AND_
- Toán tử làm việc với text: _LIKE 'string'_
- Toán tử làm việc với list: _IN, NOT IN (value1, value2,...)_
- Một số toán tử khác: _AS, TOP or LIMIT_

### 3.3. Patterns

- Ký tự `%`: Đại diện cho chuỗi ký tự có độ dài bất kỳ.
- Ký tự `_`: Đại diện cho một ký tự.
- Ký tự `[danh sách ký tự]`: Bất kỳ ký tự nào trong danh sách chỉ định.
- Ký tự `[ký tự - ký tự]`: Bất kỳ ký tự nào trong phạm vi chỉ đinh.
- Ký tự `[^]`: Bất kỳ ký tự nào ngoài danh sách.

Ngoài các ký tự trên, còn ký tự `ESCAPE`:

```sql
-- Ký tự được khai báo có thể sử dụng như ký tự escape
LIKE pattern [ESCAPE escape_character]
```

### 3.4. CASE WHEN

```sql
-- SELECT CASE WHEN
SELECT <column_list>, 
CASE 
      WHEN condition_1  THEN result_1
      WHEN condition_2  THEN result_2
      [WHEN ...]
      [ELSE else_result]
END
FROM
WHERE 
```

```sql
-- CASE expression
SELECT <column_list>, 
CASE expression
   WHEN value_1 THEN result_1
   WHEN value_2 THEN result_2 
   [WHEN ...]
ELSE
   else_result
END
FROM
WHERE 
```

## 4. JOINs

### 4.1. Một số loại Joins

JOINs được sử dụng để giúp chúng ta lấy dữ liệu từ nhiều bảng.

{{< figure src="./Joins_SQL.svg.png" width=75% >}}

### 4.2. Một số lưu ý

```sql
-- Lấy một cột cụ thể từ các bảng, ví dụ
SELECT  accounts.name,
        orders.occurred_at
FROM orders
JOIN accounts
ON orders.account_id = accounts.id;

-- Lấy tất cả các cột
SELECT *
FROM orders
JOIN accounts
ON orders.account_id = accounts.id;

-- Lấy tất cả các cột trong một bảng
SELECT orders.*
FROM orders
JOIN accounts
ON orders.account_id = accounts.id;

-- Chúng ta có thể đặt bí danh cho các bảng
FROM tablename AS t1
JOIN tablename2 AS t2

FROM tablename t1
JOIN tablename2 t2
```

### 4.3. SELF JOIN

SELF JOIN cho phép ta Join một bảng với chính nó. 

```sql
-- Sử dụng 2 alias khác nhau cho cùng một bảng 
SELECT
    select_list
FROM
    Table_name t1
[INNER | LEFT]  JOIN Table_name t2 ON
    join_predicate; 
```

### 4.4. Set Operators

```sql
query1 UNION [ALL] query2      -- Phép hợp
query1 INTERSECT [ALL] query2  -- Phép giao
query1 EXCEPT [ALL] query2     -- Phép trừ
```

{{< figure src="./set-operations.png" >}}

## 5. Aggregations

### 5.1 NULL

Trước khi đi tìm hiểu về các hàm tổng hợp dữ liệu, chúng ta cần phải quan tâm đến các giá trị NULL. NULL là một kiểu dữ liệu mang ý nghĩa không tồn tại dữ liệu trong SQL. Chúng thường bị bỏ qua trong các hàm tổng hợp.

Khi sử dụng NULL trong mệnh đề WHERE, ta sử dụng `IS NULL` hoặc `IS NOT NULL` chứ không sử dụng dấu `=`. 

### 5.2. Một số hàm tổng hợp dữ liệu

- **COUNT()**: Đếm số hàng có dữ liệu trong bảng, COUNT bỏ qua NULL.
- **COUNT(DISTINCT )**: Đếm số lượng các giá trị riêng biệt trong một cột.
- **SUM()**: Tính tổng các giá trị trong một cột, bỏ qua NULL.
- **AVG()**: Tính giá trị trung bình, bỏ qua NULL.
- **MEDIAN()**: Tính giá trị trung vị, bỏ qua NULL
- **MAX()**: Xác định giá trị lớn nhất, ngày lớn nhất hoặc giá trị không phải số gần "Z" trong bảng alphabet.
- **MIN()**: Ngược lại với MAX.

Lưu ý: Bất kỳ cột nào trong mệnh đề **SELECT** không nằm trong các hàm aggregation thì phải nằm trong mệnh đề **GROUP BY**.

### 5.3. DISTINCT

**DISTINCT** luôn nằm trong mệnh đề **SELECT**. 

```sql
-- Giá trị duy nhất của cả 3 cột
SELECT DISTINCT column1, column2, column3 
FROM table1;
```

Khi gặp giá trị **NULL, DISTINCT** sẽ giữ lại một giá trị **NULL**, các giá trị còn lại sẽ bị xóa.

## 6. Xử lý dữ liệu Date

### 6.1. DATE_PART và EXTRACT

Hai hàm này được sử dụng để trích xuất các thành phần từ kiểu dữ liệu datetime, điểm khác là **DATE_PART** là hàm của Postgresql còn **EXTRACT** là hàm áp dụng được cho nhiều DBMS:

```sql
-- Cú pháp:
DATE_PART(unit, source)
EXTRACT(unit FROM source)

-- Unit:
-- year, month, day
-- quarter, week
-- hour, minute, second
-- dow (0 - 6; Sunday is 0), doy (1 - 365/366)
```

{{< figure src="./postgresql-date_part-function.png" width=70% >}}

{{< figure src="./postgresql-extract-function.png" width=70% >}}

### 6.2. INTERVAL

**INTERVAL** được sử dụng để thêm hoặc bớt một khoảng thời gian đối với các dữ liệu datetime.

```sql
-- INTERVAL text
INTERVAL '6 years 5 months 4 days 3 hours 2 minutes 1 second';
```

### 6.3. TO_DATE

Hàm này được sử dụng để chuyển đổi một chuỗi ký tự thành datetime.

```sql
-- Cú pháp
TO_DATE(string, format_of_str)

-- Ví dụ
TO_DATE('20020304', 'YYYYMMDD')
TO_DATE('2015/06/07', 'YYYY/MM/DD')
TO_DATE('10 Feb 2017', 'DD Mon YYYY')
```

## 7. Xử lý dữ liệu Text

### 7.1. LEFT, RIGHT, LENGTH

Các hàm `LEFT()` và `RIGHT()` được sử dụng để trích xuất một phần số ký tự từ string. Còn hàm `LENGTH()` để đo độ dài của string.

```sql
-- Cú pháp
LEFT(string, number of characters)
RIGHT(string, number of characters)

-- Substring ở một vị trí xác định với độ dài length
SUBSTR(string, start, length) 

-- Độ dài của một chuỗi
LENGTH(string)
```

Hàm `TRIM()` được sử dụng để xóa một hoặc một số ký tự ở hai đầu của string.

```sql
-- Cú pháp 
-- Hàm TRIM gồm 3 thành phần:
-- Vị trí xóa: the beginning ('leading'), the end ('trailing'), or both ('both')
-- 'chrs': Tập hợp các ký tự
-- FROM column_Name: Tên cột
-- Ví dụ:
TRIM(both '()' FROM column_name)
```

### 7.2. POSITION và STRPOS

Hàm **POSITION** và **STRPOS** xác định vị trí đầu tiên xuất hiện của substring trong một chuỗi, lưu ý là cả hai hàm có phân biệt giữa các ký tự in hoa và in thường. Điểm khác nhau ở cú pháp:

```sql
-- POSITION
POSITION(substr IN colum_name)

-- STRPOS
STRPOS(column_Name, substr)
```

### 7.3. LOWER và UPPER

Hàm **UPPER** và **LOWER** chuyển đổi một chuỗi các ký tự về dạng in hoa hoặc in thường.

### 7.4. CONCAT

Hàm **CONCAT** nối các ký tự. 

```sql
-- Sử dụng hàm CONCAT
CONCAT(day_of_week, ', ', LEFT(date, 10))

-- Sử dụng toán tử ||
day_of_week || ', ' || LEFT(date, 10)
```

### 7.5. CAST

Hàm **CAST** chuyển đổi một giá trị sang một kiểu dữ liệu khác.

```sql
-- Sử dụng hàm CAST
CAST(expression AS target_type)

-- Sử dụng toán tử ::
expression::type
```

### 7.6. COALESCE

Hàm **COALESCE** trả về biểu thức có giá trị khác NULL đầu tiên:

```sql
-- Cú pháp
COALESCE(express_1,[express_2,...,express_n])

-- Sử dụng COALESCE thay thế NULL bởi NA
COALESCE(column_name, 'N/A')
```

## 8. Subqueries

Subqueries hiểu đơn giản là một truy vấn bên trong một truy vấn khác. Một số loại Subqueries thường gặp:

- Subqueries thay thế cho một biểu thức, trả về một giá trị duy nhất.
- Subqueries với toán tử `IN` hoặc `NOT IN`
- Subqueries với toán tử `ANY` hoặc `ALL`
- Subqueries với toán tử `EXISTS` hoặc `NOT EXISTS`
- Subqueries trong mệnh đề FROM, phải có Alias.
- Subqueries tương quan.

### 8.1. IN và NOT IN

```sql
scalar_expression IN (subquery)
```

Truy vấn con được trả về một tập hợp các giá trị. Sau đó chương trình sẽ lọc ra các giá trị bên trong `scalar_expression` nằm trong truy vấn con

Lưu ý khi subqueries chứa giá trị `NULL`, `NOT IN` có thể xử lý không chính xác.

### 8.2. ANY hoặc ALL

```sql
scalar_expression comparison_operator ANY|ALL (subquery)
```

Với `ANY`, giả sử truy vấn con trả về một danh sách có giá trị `V1, V1,..., Vn`. Toán tử `ANY` trả về TRUE nếu một trong các cặp so sánh (`scalar_expression`, `Vi`) trả về `TRUE`. Với toán tử `ALL` thì cần phải thỏa mãn tất cả các cặp so sánh đều trả về `TRUE`.

### 8.3. EXISTS và NOT EXISTS

```sql
WHERE [NOT] EXISTS (subquery)
```

Toán tử EXISTS sẽ trả về `TRUE` kết quả nếu subqueries trả về kết quả.

### 8.4. Subquery tương quan

Subquery tương quan là một truy vấn con sử dụng các giá trị của truy vấn bên ngoài. Một truy vấn tương quan sẽ được thực thi lặp đi lặp lại. Với mỗi hàng ở truy vấn bên ngoài, truy vấn con được lặp lại một lần.


### 8.5. Phép chia

Giả sử ta có một bảng như sau:

{{< figure src="./phep-chia.png" width=80% >}}

Ta có thể hiểu đơn giản là tìm những record `A, B, C` trong bảng _R_ sao cho, `A, B, C` kết hợp với tất cả các record `D, E` trong bảng _S_ vẫn nằm trong _R_.

Có hai cách để giải bài toán này, cách 1 sử dụng _EXCEPT_:

```sql
SELECT R1.A, R1.B, R1.C FROM R R1
WHERE NOT EXISTS (
                  SELECT S.D, S.E 
                  FROM S
                  EXCEPT
                  SELECT R2.D, R2.E 
                  FROM R R2
                  WHERE R1.A=R2.A AND R1.B=R2.B AND R1.C=R2.C
                  )
```

Cách 2, sử dụng _NOT EXIST_:

```sql
SELECT R1.A, R1.B, R1.C
FROM R R1
WHERE NOT EXISTS (
       SELECT *
       FROM S
       WHERE NOT EXISTS (
           SELECT *
           FROM R R2
           WHERE R2.D=S.D AND R2.E=S.E
           AND R1.A=R2.A AND R1.B=R2.B AND R1.C=R2.C ))
```

## 9. Temporary Tables



## 10. Window Functions
