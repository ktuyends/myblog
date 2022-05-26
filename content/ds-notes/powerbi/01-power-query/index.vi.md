---
title: "PBI - Làm quen với Power Query"
subtitle: ""
slug: intro-to-powerquery
date: 2022-05-17
lastmod: 2022-05-17
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["BI", "Power BI"]
categories: []
series: [Power BI Notes]
series_weight: 1
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

## 1. Getting data

### 1.1. Đọc dữ liệu từ file Excel

Đầu tiên, ta vào _Get Data -> Excel Workbook -> Connect_:

{{< figure src="./01-get-data/get-data-from-excel.png" width=60% >}}

Sau đó, di chuyển đến nơi lưu trữ tập dữ liệu và mở nó lên:

{{< figure src="./01-get-data/get-data-from-excel2.png" width=80% >}}

Ở bên tay trái là các bảng dữ liệu, mỗi một bảng là một Table đã được định dạng trong Excel. Bạn có thể click một bảng bất kỳ để xem trước nội dung bên trong nó. Bây giờ thì tích vào những bảng cần thiết ví dụ như _Customer, Date, Product_ và chọn **_Transform Data._**

{{< figure src="./01-get-data/get-data-from-excel3.png" width=80% >}}

Đây chính là nơi chúng ta sẽ thực hiện các hoạt động ETL trên dữ liệu. Nhưng tạm thời ta gác việc đó lại đã, ta tiếp tục với nội dung _Getting data_.

### 1.2. Đọc dữ liệu từ file CSV

Mình sẽ thêm một file CSV từ giao diện hiện có bằng cách click vào _New Source -> From Text/CSV_:

{{< figure src="./01-get-data/get-data-from-csv.png" width=80% >}}

Có một điểm ta phải chú ý ở đây là **_Delimiter_**, đây là nơi ta chỉ định ký tự phân tách giữa các cột trong file `CSV` hoặc file `TXT`. Còn **_Data Type Detection_** nói rằng Power Query sẽ xác định kiểu dữ liệu của mỗi cột dựa vào cơ sở nào đó, ví dụ như trong hình là dựa vào 200 hàng đầu tiên.

Đến đây, bạn có thể click vào **_OK_** để thêm bảng vào trong PQ hoặc click vào _Extract Table Using Examples_ để trích một phần nội dung từ trong bảng. Nhập tên cột muốn lấy và nhập một vài giá trị trong cột để PQ có thể nhận diện tự động:

{{< figure src="./01-get-data/get-data-from-csv2.png" width=100% >}}

### 1.3. Đọc dữ liệu từ folder

Sau khi đã nghịch chán với việc đọc từng file một. Chúng ta chơi lớn hơn, đọc toàn bộ dữ liệu bên trong một thư mục. Giả sử ta có dữ liệu bán hàng của từng ngày, mỗi ngày được lưu trong một file và dĩ nhiên cấu trúc của các file này là giống nhau.

Ví dụ ở đây mình có hai thư mục, một thư mục cho các file `CSV` và một thư mục cho các file `Excel`:

{{< figure src="./01-get-data/get-data-from-folder.png" width=60% >}}

{{< figure src="./01-get-data/get-data-from-folder2.png" width=60% >}}

Vẫn tương tự như đọc file, ta chọn _Get Data -> From Folder_, di chuyển đến folder chứa dữ liệu và chọn _OK_:

{{< figure src="./01-get-data/get-data-from-folder3.png" width=80% >}}

Click vào _Transform Data_:

{{< figure src="./01-get-data/get-data-from-folder4.png" >}}

Đến đây, ta có một số lựa chọn:

- Click vào Binary ở cột Content để xem một file cụ thể.
- Click vào Icon ở cột Attributes để lựa chọn các cột dữ liệu.
- Click vào Icon _(hai cái mũi tên đi xuống)_ ở cột Content để kết hợp các file lại với nhau.

Chúng ta sẽ bàn về Combine dữ liệu ở phần sau, bây giờ đi tìm hiểu cách đọc dữ liệu từ Database.

### 1.4. Đọc dữ liệu từ database

Để đọc dữ liệu từ database, ta chọn đến nguồn CSDL mà bạn sử dụng, ở đây mình sử dụng SQL Server:

{{< figure src="./01-get-data/get-data-from-database.png" width=70% >}}

Chúng ta sẽ có hai lựa chọn:

- Một là lựa chọn các bảng từ CSDL như ta đã làm với các loại file khác.
- Hai là lựa chọn các bảng từ câu truy vấn SQL.

Và nếu để ý bạn sẽ thấy có hai chế độ:

- _Import_: Các dữ liệu được nạp từ CSDL vào trong Power Query. Với các dữ liệu này ta có thể chỉnh sửa và tạo ra các mối quan hệ giữa các bảng với nhau.
- _DirectQuery_: Phương thức này không nạp dữ liệu vào trong Power Query, dữ liệu vẫn ở trên CSDL. Power Query chỉ thực hiện các truy vấn lên CSDL để lấy các dữ liệu cần thiết.

Sau khi import dữ liệu vào trong PQ, các bạn hoàn toàn có thể chỉnh sửa câu truy vấn ở _**Advanced Editor**_.

{{< figure src="./01-get-data/get-data-from-database2.png" width=90% >}}

### 1.5. Đọc dữ liệu từ website

Giả sử ta muốn lấy dữ liệu từ trang [PacktPub](https://www.packtpub.com/eu/all-products)

{{< figure src="./01-get-data/get-data-from-web.png" width=80% >}}

{{< figure src="./01-get-data/get-data-from-web2.png" width=80% >}}

Ta cũng có thể thêm các tùy chọn lọc bằng phần **_Advanced_** như sau:

{{< figure src="./01-get-data/get-data-from-web3.png" width=80% >}}

## 2. Data exploration

### 2.1. Lựa chọn columns

Sau khi nạp dữ liệu vào trong Power Query, việc đầu tiên chúng ta nên làm là suy nghĩ về việc lựa chọn ra những cột cần thiết cho quá trình chuẩn bị dữ liệu và xóa những cột còn lại.

**_Manage Columns_** trong tab Home sẽ cho chúng ta một số lựa chọn:

- _Choose Columns_: Click để lựa chọn những cột mà ta cần.
- _Remove Columns_: Xóa những cột đang được chọn.
- _Remove Other columns_: Tùy chọn này sẽ giữ lại những cột đang được chọn và xóa các cột còn lại.

Tùy chọn _Remove Columns_ cũng xuất hiện khi bạn click chuột phải vào một cột hoặc một dãy các cột được lựa chọn.

Để lựa chọn nhiều cột, tương tự như trong Excel, ta sử dụng phím `Shift` nếu muốn chọn một dãy các cột hoặc phím `Ctrl` nếu muốn chọn từng cột riêng lẻ.

### 2.2. Data profiling

Data Profiling, ta hiểu đơn giản là các bước kiểm tra chất lượng của tập dữ liệu. Trong PQ, Có một số tùy chọn giúp chúng ta thực hiện việc này.

Đầu tiên là tùy chọn _Column Quality_ ở trong Tab View mà khi ta lựa chọn sẽ được kết quả như hình sau:

{{< figure src="./02-data-exploration/data-profilling.png" >}}

Quan sát hình trên ta có một số thông tin:

- _Valid_: Tỷ lệ phần trăm dữ liệu hợp lệ.
- _Error_: Tỷ lệ phần trăm dữ liệu bị lỗi.
- _Empty_: Tỷ lệ phần trăm của các hàng trống.
- _Column profiling based on top 1000 rows_: Kết quả profiling dựa vào 1000 hàng đầu tiên của bảng dữ liệu. Các bạn có thể click vào dòng này để thay đổi thành toàn bộ các hàng.

Sau khi đổi profiling dựa vào tất cả các hàng, một lỗi đã xuất hiện (di chuyển vào thông tin profiling):

{{< figure src="./02-data-exploration/data-profilling2.png" width=70% >}}

Để xem thông tin về hàng nào gây ra lỗi, hãy click chuột phải vào bảng kết quả và chọn _Kept Errors -> Errors_

{{< figure src="./02-data-exploration/data-profilling3.png" width=70% >}}

Ồ hóa ra là có giá trị `480b` bị lỗi. Chúng ta quay lại bảng profiling, click chuột phải và chọn _Replace Error_ để thay đổi giá trị mới cho giá trị bị lỗi.

Tùy chọn data profiling tiếp theo là **_Column distribution_** và **_Column profile_**:

{{< figure src="./02-data-exploration/data-profilling4.png" >}}

## 3. Reshaping data

## 4. Combining queries

## 5. Optimizing queries

## 10. Tóm tắt

Tóm tắt lại, một số bước chúng ta có thể làm với Power Query như sau:

- Nạp dữ liệu vào Power Query (Get data):
  - _Một file_
  - _Một folder_
  - _Một database_
  - _Một website_
- Lựa chọn và xóa các cột không cần thiết (Manage Column).
- Kiểm tra chất lượng từng cột dữ liệu (View tab):
  - _Column quality_
  - _Column distribution_
  - _Column profile_
