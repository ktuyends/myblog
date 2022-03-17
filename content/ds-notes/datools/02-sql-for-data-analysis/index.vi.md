---
title: "DA Tools - SQL for data analysis"
subtitle: ""
slug: sql-for-data-analysis
date: 2022-02-25
lastmod: 2022-02-25
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

## 1. Cài đặt và kết nối với server

Để làm việc với SQL Server, ta cần cài đặt:

- [SQL Server Developer](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15)

Sau khi cài đặt xong, ta bật SSMS (SQL Server Management Studio) và đăng nhập để kết nối với server.

## 2. Tạo cơ sở dữ liệu

### 2.1. Tạo CSDL đơn giản

Để tạo CSDL, ta click chuột phải vào *Databases* và chọn *New Database*, sau đó nhập tên của CSDL mới:

{{< figure src="create-csdl.png" >}}

### 2.2. Tạo một bảng đơn giản

{{< figure src="create-table.png" >}}

Để tạo một bảng, chúng ta click chuột phải vào *Table* và chọn *New Table*. Sau đó, chúng ta nhập vào các thông tin của bảng bao gồm:

- Column Name: Tên cột
- Data Type: Kiểu dữ liệu của cột
- Allow Nulls: Có cho phép giá trị Null hay không

Khi nhập xong các dữ liệu cần thiết, ta click vào *Save* và đặt tên bảng để hoàn thành.

**Một số kiểu dữ liệu cơ bản trong SQL Server:**

| Kiểu dữ liệu | Ý Nghĩa |
|:-:|-|
| CHAR(10) | Chuỗi ký tự với độ dài cố định là 10 |
| NCHAR(10) | Tương tự char, nhưng có thể bao gồm các ký tự Unicode |
| VARCHAR(50) | Chuôi ký tự với độ dài tùy biến, tối đa là 50|
| NVARCHAR(50) | Tương tự nvarchar, nhưng có thể bao gồm các ký tự Unicode|
| TEXT | Chuỗi có chứa độ dài tùy biến, không bao gồm các ký tự Unicode |
| NTEXT | Chuỗi có độ dài tùy biến, có thể bao gồm các ký tự Unicode |
| TINYINT/SMALLINT/INT/BIGINT | Số nguyên với các phạm vi khác nhau|
| DECIMAL | Lưu trữ số thực có giá trị chính xác |
| FLOAT | Lưu trữ số thực có giá trị xấp xỉ |
| DATE/TIME/DATETIME| Kiểu dữ liệu ngày tháng - thời gian|


{{< admonition type=notes title="Một số lưu ý khi tạo bảng" open=true >}}

- Đặt tên bảng với tiền tố bắt đầu bằng tbl, ví dụ: *tbl_Customer*
- Với tên cột, trường, sử dụng chữ viết tắt của tên bảng làm tiền tố
- Trường khóa: Sử dụng kiểu dữ liệu là *uniqueidentifier*
- Một số trường nên sử dụng giá trị mặc định như: *newid(), getdate()*
{{< /admonition >}}

### 2.3. Nhập dữ liệu vào bảng

**Cách 1: Sử dụng SSMS**

Để nhập dữ liệu vào bảng, ta click chuột phải vào bảng cần nhập và chọn *Edit Top 200 Rows*

**Cách 2: Nhập dữ liệu từ file CSV**

Để nhập dữ liệu từ file CSV, ta click chuột phải vào database, sau đó chọn: *Task -> Import Data -> Data source: Flat File Source -> ...*. 

### 2.4. Tạo CSDL từ CSDL mẫu

Giả sử ta có một CSDL mẫu hoặc một CSDL được sao lưu từ một máy chủ nào đó, bây giờ chúng ta muốn thêm nó vào server hiện tại, ta click chuột phải vào *Databases* và chọn: *Restore Database*

{{< figure src="ssms-restore.png" >}}

### 2.5. Tạo bảng từ file CSV

Để tạo bảng từ file CSV, ta click chuột phải vào database, sau đó chọn: *Task -> Import Flat File*

{{< figure src="import-data.png" >}}

### 2.6. Tạo bảng bằng câu lệnh

```sql
-- Tạo Database LearnDS
CREATE DATABASE LearnDS;
GO

-- Sử dụng Database LearnDS
USE LearnDS;
GO
```

```sql
-- Tạo một bảng 
-- m là giá trị bắt đầu, n là giá trị tăng thêm
CREATE TABLE [database_name.][schema_name.]table_name (
    pk_column data_type PRIMARY KEY IDENTITY (m, n),
    column_1 data_type NOT NULL,
    column_2 data_type UNIQUE,
    column_3 data_type DEFAULT GETDATE(),
    ...,
    table_constraints
);

-- Một vài ví dụ dòng ràng buộc constraints
-- Khóa chính
CONSTRAINT pk_ma_ts PRIMARY KEY (MaTaiSan),

-- Khóa ngoại
CONSTRAINT FOREIGN KEY (MaKH) REFERENCES KhachHang(MaKH),
```

### 2.7. Nhập dữ liệu bằng câu lệnh

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

***Ví dụ:***

```sql
-- Tạo bảng sales.promotions
CREATE TABLE sales.promotions (
    promotion_id INT PRIMARY KEY IDENTITY (1, 1),
    promotion_name VARCHAR (255) NOT NULL,
    discount NUMERIC (3, 2) DEFAULT 0,
    start_date DATE NOT NULL,
    expired_date DATE NOT NULL
); 

-- Nhập dữ liệu
INSERT INTO sales.promotions (
    promotion_name,
    discount,
    start_date,
    expired_date
)
VALUES
    (
        '2019 Summer Promotion',
        0.15,
        '20190601',
        '20190901'
    ),
    (
        '2019 Fall Promotion',
        0.20,
        '20191001',
        '20191101'
    ),
    (
        '2019 Winter Promotion',
        0.25,
        '20191201',
        '20200101'
    );
```

## 3. Truy vấn dữ liệu
