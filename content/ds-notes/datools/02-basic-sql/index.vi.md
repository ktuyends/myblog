---
title: "DA Tools - SQL cơ bản"
subtitle: ""
slug: basic-sql
date: 2021-12-15
lastmod: 2021-12-15
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["DA Tools"]
categories: []
series: [Data Analysis Tools]
series_weight: 2
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

## 1. Một số khái niệm về CSDL Quan Hệ

Dữ liệu được thể hiện ở dưới dạng bảng, trong một CSDL thường sẽ có rất nhiều bảng dữ liệu có quan hệ và được liên kết với nhau thông qua mô hình ERD (Mô hình thực thể kết hợp, hoặc mô hình thực thể liên kết). Mỗi bảng dữ liệu, chứa thông tin về một thực thể (đối tượng) nào đó. 

Một bảng dữ liệu sẽ gồm các hàng và các cột. 

- Các hàng đôi khi còn được gọi là các bản ghi (record). 
- Các cột đôi khi còn được gọi là các trường (field) hoặc các thuộc tính (attribute)

Ví dụ một bảng dữ liệu:

{{< figure src="table.png" >}}

Trong mỗi bảng dữ liệu bắt buộc sẽ phải có khóa chính (Primary Key - PK). Khóa chính là một cột hoặc tổ hợp các cột, xác định mỗi hàng là duy nhất. Nghĩa là, với mỗi hàng hoặc bản ghi, giá trị của khóa chính là duy nhất và không được trống (NULL).

Hai bảng muốn liên kết được với nhau phải có một điểm chúng nào đó. Khóa ngoại (Foreign Key - FK) là điểm chung đó. Nó là chìa khóa để liên kết hai bảng với nhau. Về cơ bản, khóa ngoại (FK) sẽ là PK ở một bảng nhưng lại là FK ở bảng khác mà bảng đó liên kết.

Mô hình ERD thể hiện mối quan hệ giữa các bảng, ta có 3 kiểu mối quan hệ:

- Mối quan hệ 1-1: Nếu với mỗi thực thể trong bảng A chỉ tương ứng với 1 thực thể trong bảng B, và ngược lại.
- Mối quan hệ 1-N: Nếu với mỗi thực thể trong bảng A có thể tương ứng với nhiều thực thể trong bảng B, nhưng một thực thể trong bảng B chỉ có thể tương ứng với 1 thực thể trong bảng A.
- Mối quan hệ N-N (1-N, N-1): Nếu một thực thể trong bảng A, có thể tương ứng với nhiều thực thể trong bảng B và ngược lại. Thường thì giữa bảng A và bảng B, sẽ có một bảng C làm mối quan hệ cầu nối như `A (1) - (N) C (N) - (1) B`

## 2. Câu Lệnh SELECT

### Cú pháp

Về cơ bản, câu lệnh SELECT có cấu trúc như sau, trong đó SELECT là bắt buộc, nó có thể đứng độc lập một mình, các câu lệnh còn lại là tùy chọn.

```sql
-- schema.table có cấu trúc kiểu: 
-- network.database_name.table_name.column_name
SELECT [columns to return]
FROM [schema.table]
WHERE [conditional filter statements]
GROUP BY [columns to group on]
HAVING [conditional filter statements that are run after grouping]
ORDER BY [columns to sort on] ASC/DESC
LIMIT [maximum number of rows that are returned]

-- MYSQL sử dụng LIMIT
-- SQL Server sử dụng SELECT TOP n
```

Thứ tự logic thực hiện của các câu lệnh trên: FROM > WHERE > GROUP BY > HAVING > SELECT > ORDER BY.

### Tính toán trong câu lệnh SELECT

Có thể sử dụng các phép tính đơn giản hoặc các built-in functions như:

```sql
-- Các phép tính: +, -, *, /
SELECT Column_A + Column_B, Func_name(parameters)
```

### Alias

Chúng ta có thể gán tên cho các cột, hoặc đặt tên cho cột mới được tạo ra bởi các phép tính bằng Alias:

```sql
-- Ví dụ:
SELECT Columns AS new_name, Calculations AS new_name
```

Nếu Alias chứa khoảng trắng, ta cần phải bao nó bởi dấu ngoặc kép `"new name"` hoặc dấu ngoặc vuông `[new name]`. Trong nhiều hệ quan trị CSDL, ta có thể đặt tên ngay phía sau cột vì nó sẽ ngầm hiểu đó là Alias, nhưng tôi nghĩ là nên viết `AS` cho cú pháp được rõ ràng.

## 3. Câu lệnh WHERE

Câu lệnh WHERE được sử dụng để lọc dữ liệu. Nếu như bạn từng sử dụng các ngôn ngữ lập trình khác, thì nó gần giống với câu lệnh IF, sử dụng các toán tử logic ví dụ như AND, OR,...

Các toán tử so sánh trong SQL:

| Toán Tử | Mô Tả |
|--|--|
| = | Ngang bằng |
| != | Không bằng |
| > | Lớn hơn|
| >= | Lớn hơn hoặc bằng |
| < | Nhỏ hơn |
| <= | Nhỏ hơn hoặc bằng |

Các toán tử logic:

| Toán Tử | Mô Tả |
|--|--|
| AND | Toán tử và |
| OR | Toán tử hoặc |
| NOT| Toán tử phủ định |

Các toán tử khác:

| Toán Tử | Mô Tả |
|--|--|
| BETWEEN...AND... | Lọc các hàng nằm trong khoảng nào đó |
| IN (value1, value2,...) | Lọc các hàng có giá trị nằm trong list |
| ANY () |  |
| ALL () |  |
| LIKE | So Sánh chuỗi, % đại diện cho số lượng ký tự bất kỳ |
| IS NULL | Kiểm tra xem các rows có giá trị NULL không |
|IS NOT NULL | Phủ định của IS NULL |


> Lưu ý 1: NULL là giá trị thiếu, không phải khoảng trắng. Khoảng trắng là có giá trị thuộc kiểu dữ liệu text. NULL không thể thực hiện các phép so sánh và tính toán, mọi so sánh và tính toán sẽ trả về NULL. Như vậy trong SQL, ngoài TRUE và FALSE ta còn NULL. Câu lệnh WHERE chỉ lựa chọn các hàng trả về TRUE. 


> Lưu ý 2: Câu lệnh WHERE không thể lọc các điều kiện với các cột dữ liệu mới được tạo ra trong câu lệnh SELECT bởi các hàm, các phép tính. Vì câu lệnh SELECT thực thi sau WHERE nên các dữ liệu đó chưa được tạo thành. Khi đó, để áp dụng các điều kiện cho các cột mới này, ta phải dùng Subqueries (truy vấn con)

## 4. Câu lệnh CASE

Câu lệnh CASE, được sử dụng để tạo ra một cột mới, dựa trên một số điều kiện nào đó, cú pháp như sau:

```sql
CASE
   
 WHEN [first conditional statement] 
     
 THEN [value or calculation]
   
 WHEN [second conditional statement] 
     
 THEN [value or calculation]
   
 ELSE [value or calculation]
END AS new_column_name
```

## 5. SQL JOINs

Trong các câu lệnh trên, chúng ta mới chỉ tập chung làm việc với một bảng duy nhất. Nhưng thực tế, thì dữ liệu chúng ta cần lấy nó lại nằm ở rất nhiều nơi. Vì vậy, ta cần phải kết hợp thông tin của các bảng lại với nhau. Trong phần này, ta sẽ đi tìm hiểu câu lệnh JOINs, đây là câu lệnh sẽ giúp chúng ta giải quyết vấn đề vừa được nêu ra.

Cú pháp:

```sql
-- JOIN TYPE: LEFT JOIN, RIGHT JOIN, INNER JOIN, FULL JOIN
SELECT [columns to return]
FROM [left table] [JOIN TYPE] [right table]
ON [left table].[field in left table to match] = [right table].[field in right table to match]
```

Bốn loại JOINs phổ biến:

- LEFT JOIN: Lấy toàn bộ dữ liệu trong left_table, và chỉ lấy những giá trị khớp được từ right_table, những hàng nào không được khớp sẽ trả về NULL
- RIGHT JOIN: Ngược lại với LEFT JOIN
- INNER JOIN: Chỉ lấy toàn bộ những hàng khớp được với nhau từ hai bảng
- FULL JOIN: Khớp và lấy toàn bộ dữ liệu từ hai bảng, những hàng nào không được khớp sẽ trả về NULL
- Ngoài ra còn có CROSS JOIN, CROSS APPLY, OUTER APPLY nhưng ít được sử dụng

Một số vấn đề với JOINs:

- Một số phép JOIN sẽ trả về giá trị NULL ở một số hàng. Hãy nhớ lại logic thực hiện trong SQL là từ FROM rồi mới đến WHERE. Vì vậy, khi bảng được kết hợp từ các bảng trong câu lệnh FROM có chứa giá trị NULL, câu lệnh WHERE sẽ bỏ qua hết những hàng này.
- Vấn đề thứ hai, trong một số trường hợp, kết quả trả về có thể chứa các hàng trùng lặp. Để giải quyết vấn đề này có thể sử dụng câu lệnh sau:
- Lệnh JOIN có thể liên kết nhiều bảng với nhau, không chỉ hai bảng. Thứ tự thực hiện từ trên xuống dưới.

```sql
SELECT DISTINCT columns
```

## 6. Câu lệnh GROUP BY

Trong các phần trên, chúng ta mới chỉ thực hiện lấy dữ liệu từ nhiều bảng. Nhưng các dữ liệu chỉ ở dạng thô, không cung cấp quá nhiều thông tin. Nếu bây giờ, bạn muốn tổng hợp dữ liệu theo một số chỉ tiêu nào đó thì phải làm thế nào. Ví dụ như doanh thu theo khu vực, theo giới tính,...Đừng lo lắng, GROUP BY sẽ giúp chúng ta giải quyết vấn đề này.

Cú pháp:

```sql
SELECT [columns to return]
FROM [schema.table]
WHERE [conditional filter statements]
GROUP BY [columns to group on]
HAVING [conditional filter statements that are run after grouping]
```

Khi sử dụng GROUP BY, chúng ta thường sẽ sử dụng kèm theo một số hàm tổng hợp dữ liệu ví dụ như Đếm số lượng, tính tổng số lượng,...

| Tên Hàm | Mô tả |
|-|-|
| DISTINCT | Loại bỏ hàng trùng lặp |
| ROUND() | Làm tròn số |
| COUNT() | Đếm số hàng |
| COUNT(DISTINCT ) | Đếm giá trị duy nhất|
| SUM() | Tính tổng |
| MIN() | Giá trị nhỏ nhất |
| MAX() | Giá trị lớn nhất |
| AVG() | Giá trị trung bình |
| UPPER() | Chuyển các ký tự về in hoa |
| LOWER() | Chuyển các ký tự về in thường|


> Trong SQL Server còn hỗ trợ GROUPING SETS, GROUP BY theo một tập hợp các group khác nhau. Có thể hiểu đơn giản là nó giống như ta thực hiện rất nhiều truy vấn theo từng nhóm, sau đó thực hiện UNION ALL. Ngoài GROUPING SETS, SQL Server còn có CUBE, ROLLUP...


## 7. Window Functions

Window Functions tương tự như các hàm Aggregate Function (SUM, AVG, COUNT), nhưng điểm khác biệt là các row sẽ không bị gộp lại như khi dùng các hàm tổng hợp dữ liệu, cú pháp:

```sql
SELECT
WINDOW_FUNCTION() () OVER (PARTITION BY Column_A ORDER BY Column_B ASC/DESC)
```

Giải thích:

- OVER(): là để chỉ ra đây là một Window Function
- PARTITION BY: Gom các hàng có cùng giá trị vào một nhóm. Khi gọi PARTITION BY thì windows function sẽ áp dụng cho các nhóm riêng biệt. Còn khi không gọi PARTITION BY thì sẽ áp dụng cho tất cả các hàng trong cột ORDER BY.
- ORDER BY: Sắp xếp lại dữ liệu trước khi thực thi hàm

Một số hàm Window Functions:

| Tên Hàm | Mô tả |
|-|-|
| ROW_NUMBER | Đánh số xếp hạng, mỗi hàng là một thứ hạng |
| RANK | Tương tự như ROW_NUMBER, nhưng giá trị cùng nhau sẽ có thứ hạng bằng nhau, ví dụ 1, 2, 2, 4|
| DENSE_RANK | Tương tự như RANK, nhưng không nhảy thứ hạng, ví dụ 1, 2, 2, 3|
| NTILE(n) | Chia mỗi cột thành n phần bằng nhau, và đánh số mỗi nhóm từ 1 đến n|
| SUM(Column) | Tính tổng, nếu có ORDER BY, sẽ tính tổng tích lũy, ORDER BY bỏ qua hàng có giá trị trùng lặp |
| COUNT(Column) | Đếm số hàng, nếu có ORDER BY sẽ đếm số tích lũy |
| AVG(Column) | Tương tự như SUM, chỉ khác là tính trung bình |
| LAG(Column, offset, default) | Truy cập các giá trị phía trước offset đơn vị, default giá trị thay thế NULL |
| LEAD(Column, offset, default) | Tương tự LAG, nhưng truy cấp các giá trị phía sau |

## 8. CTEs and Views

Trong phần này, ta sẽ đi tìm cách để lưu kết quả truy vấn cho phép chúng ta sử dụng lại khi cần thiết.

**Câu lệnh WITH:**

```sql
-- Lưu kết quả queries vào các alias
WITH [query_alias] AS
(
[query]
),
[query_2_alias] AS
(
[query_2]
)

-- Sử dụng lại kết quả
SELECT [column list]
FROM [query_alias]
… [remainder of query that references aliases created above]
```

**Câu lệnh Views:**

```sql
CREATE VIEW [schema_name].[view_name] AS
SELECT
FROM
WHERE
```

> Lưu ý: CTEs sẽ kết thúc sau khi câu truy vấn được hoàn thành. Ngược lại View có thể sử dụng nhiều lần trong các câu truy vấn khác nhau. Hiểu đơn giản thì CTEs sẽ tạo ra một bảng tạm thời, còn View sẽ không tạo bảng mà nó sẽ tham chiếu trực tiếp đến câu truy vấn.

## 9. Set Operators

Cú pháp:

```sql
query_A

Set_operators --UNION, UNION ALL, INTERSECT, EXCEPT

query_B
```

Khi sử dụng Set Operators, yêu cầu các truy vấn phải có cùng số cột, tên các cột giống nhau và các kiểu dữ liệu trong các cột phải tương tự nhau. Một số Set Operators trong SQL (Logic giống các phép toán tập hợp):

Phép hợp: UNION (Loại bỏ các hàng trùng lặp), UNION ALL (Lấy tất cả các hàng)
Phép giao: INTERSECT
Phép trừ: EXCEPT

## 10. Subqueries

Subquery (truy vấn con, truy vấn lồng), hiểu đơn giản là một truy vấn được lồng vào bên trong một truy vấn khác. Bạn có thể sử dụng truy vấn con ở một số nơi như:

- Subquery thay thế cho một biểu thức
- Subquery trong mệnh đề FROM
- Subquery với toán tử IN hoặc NOT IN
- Subquery với toán tử ANY hoặc ALL
- Subquery với toán tử EXISTS hoặc NOT EXISTS

Truy vấn con có thể chia làm hai loại:

- Truy vấn con độc lập với truy vấn bên ngoài
- Truy vấn con có tương quan với truy vấn bên ngoài, trong trường hợp này, với mỗi hàng trong truy vấn bên ngoài, truy vấn con sẽ thực thi một lần.

**Lưu ý khi sử dụng EXISTS và NOT EXISTS:**

Toán tử EXISTS sẽ trả về TRUE nếu kết quả truy vấn trả về một giá trị bất kỳ. EXISTS thường được sử dụng khi thực hiện truy vấn các phép chia trong SQL.

Trong SQL, hình như chưa có toán tử hỗ trợ phép chia. Vì vậy, ta cần phân tích nó thành phép trừ. Giả sử ta có hai bảng như sau:

Bảng Skill:

|skill|
|-|
|Oracle|
|UNIX|
|Java|

Bảng EmpSkills:

| emp | skill |
|-|-|
| Aida | Oracle |
| Aida | UNIX |
| Aida | Java |
| Aida | C# |
| Kanzaki | Oracle |
| Kanzaki | UNIX |
| Kanzaki | Java |
| Hirai | UNIX |
| Hirai | Oracle |
| Hirai | PHP |
| Hirai | Perl |
| Hirai | C++ |
| Wakatabe | Perl |
| Torai | Oracle |

Mục tiêu của ta là tìm những nhân viên từ bảng EmpSkills có tất cả những kỹ năng xuất hiện trong bảng Skill. Phân tích:

Với mỗi nhân viên từ EmpSkills, ta lọc ra tất cả các kỹ năng của nhân viên đó. Rồi thực hiện phép trừ Bảng Skill với bảng này, nếu kết quả là rỗng, chứng tỏ nhân viên đó có tất cả những kỹ năng xuất hiện trong bảng Skill. Trong SQL:

```sql
SELECT emp
FROM EmpSkills AS es1
WHERE NOT EXIST (
    SELECT skill
    FROM Skill

    EXCEPT

    SELECT skill
    FROM EmpSkills AS es2
    WHERE es2.emp = es1.emp
)
```
