---
title: "ETB - Excel cơ bản"
subtitle: ""
slug: excel-notes
date: 2022-02-25
lastmod: 2022-02-25
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Excel"]
categories: []
series: [Excel - Tableau]
series_weight: 1
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

## 1. Một số thao tác cơ bản

### 1.1. Data validation

Data validation được sử dụng để:

- Hạn chế dữ liệu nhập vào trong một ô bằng các tiêu chí.
- Đưa ra các cảnh báo nếu dữ liệu nhập sai.
- Đưa ra gợi ý về dữ liệu cần nhập.
- Data validation sẽ bị hủy nếu người dùng paste dữ liệu vào ô.

### 1.2. What-If analysis

**Scenario Manager**: Tạo ra các kịch bản và với mỗi kịch bản sẽ có một cột input ảnh hưởng đến output.

**Data Table**: Cho phép chúng ta xem sự thay đổi giá trị trong một ô output với các giá trị khác nhau của một hoặc hai ô input được xác định.

{{< figure src="what-if2.png" width=70% >}}

**Goal Seek**: Giải phương trình, giả sử ta có một output xác định và ta cần đi tìm input tương ứng.

### 1.3. Text to columns

Text-to-columns được sử dụng để phân tách dữ liệu trong một cột thành nhiều cột khác nhau dựa vào các ký tự đặc biệt như dấu `,` hoặc tab,...hoặc độ dài cố định của các ký tự.

### 1.4. Flash fill

Flash Fill cho phép chúng ta tách dữ liệu trong một cột thành nhiều cột khác nhau, dựa vào pattern trong hàng đầu tiên. Nó không dựa vào công thức nên có đôi khi sẽ không chính xác với những gì chúng ta mong muốn.

{{< figure src="flash-fill.jpg" width=70% >}}

### 1.5. Các hàm hay sử dụng

- Hàm tổng hợp dữ liệu: _SUM(), COUNT(), MIN(), MAX(), AGGREGATE(), SUBTOTAL()_
- Hàm Logic: _AND(), OR(), NOT(), IF()_
- Hàm thống kê: _AVERAGE(), MEDIAN(), MODE(), STDEV()_
- Hàm điều kiện: _SUMIF(), COUNTIF(), AVERAGEIF()_
- Hàm text: _UPPER(), LOWER(), PROPER(), LEFT(), RIGHT(), MID()_
- Hàm nối: _CONCATENATE()_
- Hàm thời gian: _NOW(), TODAY(), DATE(), TIME()_
- Hàm tham chiếu: _VLOOKUP(), INDEX(array, row, col), MATCH(lookup_value, array, type), INDIRECT()_

### 1.6. Quick analysis

**Quick analysis:** là một tính năng đưa ra một số gợi ý giúp chúng ta thực hiện các phân tích dữ liệu một cách nhanh chóng.

{{< figure src="quick-analysis-tool.png" width=70% >}}

### 1.7. Subtotals

**Subtotals:** là một tính năng tổng hợp dữ liệu theo từng giá trị định tính trong một cột xác định.

{{< figure src="subtotals-excel.png" width=40% >}}

### 1.8. Tables

Tables trong Excel là một đối tượng đặc biệt được đặt tên và cho phép chúng ta quản lý nội dung bên trong một cách độc lập với phần còn lại của trang tính.

{{< figure src="tables.png" width=75% >}}

Tham chiếu đến dữ liệu trong Tables:

- _tbl_name[#All]_: Tham chiếu đến toàn bộ bảng bao gồm header, data, total.
- _tbl_name[#Headers]_: Tham chiếu đến toàn bộ tên cột.
- _tbl_name[#Data]_: Tham chiếu đến toàn phần data của bảng.
- _tbl_name[#Totals]_: Tham chiếu đến hàng total nếu nó tồn tại.

Tham chiếu đến dữ liệu trong một hàng hoặc cột của Table:

- _tbl_name[[#All], [Column2]]_: Tham chiếu đến toàn bộ dữ liệu trong một cột.
- _tbl_name[Column2]_: Tham chiếu đến phần data trong cột Column2.
- _tbl_Table1[@Column2]_: Tham chiếu đến giá trị tương ứng trong Column2 mà cùng dòng với ActiveCell.
- _tbl_Table1[@]_: Tham chiếu đến toàn bộ hàng hiện tại trong Column2 mà cùng dòng với ActiveCell.

### 1.9. Làm việc với mảng

Spill Range là một tính năng mới của Excel, ta có thể hiểu đơn giản là nó sẽ trả về nhiều kết quả trên một vùng mà chỉ cần thông qua một công thức. Công thức này còn được gọi là công thức mảng động.

{{< figure src="array.png" width=75% >}}

Một số hàm mảng động:

- _FILTER()_: Lọc dữ liệu thỏa mãn một điều kiện nào đó.
- _SORT()_: Sắp xếp các giá trị của một mảng.
- _SORTBY()_: Sắp xếp các giá trị của một mảng dựa vào một mảng khác.
- _UNIQUE()_: Trả về các giá trị duy nhất trong một mảng.
- _RANDARRAY()_: Một mảng các số ngẫu nhiên.
- _SEQUENCE()_: Tạo một mảng các số tăng dần.
- _XLOOKUP()_: Hàm tham chiếu.
- _XMATCH()_: Hàm tham chiếu.

### 1.10. Một số tính năng khác

- Sort and Filter
- Conditional Formatting
- Chart
- PivotTable
- PivotChart
- Shapes

## 2. Power Query

{{< figure src="excel-process.png" width=75% >}}

### 2.1. Get & Transform Data

Trước khi đi vào phân tích dữ liệu, chúng ta cần phải load data vào Excel. Như trước đây, chúng ta thường sẽ vào Menu _File -> Open_ thì bây giờ, ta làm quen với các công cụ tiên tiến hơn như _Get & Transform Data_:

{{< figure src="get-data.png" width=75% >}}

Ví dụ, để đọc một file CSV, ta chọn _From Text/CSV_:

{{< figure src="get-csv.png" width=85% >}}

Như các bạn thấy, một bảng mới hiện ra, cung cấp cho chúng ta một số thông tin:

- _Delimiter_: Ký tự phân tách giữa các cột.
- _Data Type Detection_: Kiểu dữ liệu trong các cột được xác định dựa trên 200 hàng đầu tiên.
- _Transform Data_: Đưa chúng ta vào giao diện của Power Query để thực hiện các thao tác biến đổi dữ liệu.
- _Load_: Nếu các bạn cảm thấy chưa cần chỉnh sửa thì chúng ta chọn _Load_ để nhập dữ liệu vào trong Excel. Khi chọn _Load_ cửa sổ _Import data_ được bật ra và cung cấp cho chúng ta một số lựa chọn.

{{< figure src="close.png" width=60% >}}

Ở đây, chúng ta có hai hướng chính:

- Hướng thứ nhất, lưu trữ dữ liệu vào một vùng trong Excel dưới dạng bảng như Tables,...
- Hướng thứ hai, không lưu trữ dữ liệu mà chỉ tạo kết nối với dữ liệu thông qua _Only Create Connection_.

Ở phía dưới cùng của cửa sổ, có một hộp tick _Add this data to the Data Model_, tùy chọn này được sử dụng khi chúng ta làm việc với nhiều bảng và cần các kết nối giữa các bảng với nhau.

Sau khi load data, đây là kết quả của chúng ta:

{{< figure src="./load-result.png" width=85% >}}

Khi bạn nhìn vào khu vực _Queries & Connections_, và cảm thấy không thích tên Query được tạo ra tự động bởi Excel. Bạn click chuột phải vào Query chọn _Rename_ và đổi tên cho nó.

### 2.2. Nhập dữ liệu từ một thư mục

Giả sử chúng ta có một thư mục gồm rất nhiều files, và các files có cấu trúc giống nhau (nghĩa là trong các bảng, các cột có cùng tên với nhau). Với Power Query, chúng ta có thể đọc và merge tất cả các files này với nhau. Để làm điều đó, ta chọn _Get Data -> From File -> From Folder..._

{{< figure src="./get-folder.png" width=85% >}}

Chọn _Combine & Transform Data_:

{{< figure src="./get-folder2.png" width=85% >}}

Bây giờ, ta phải chọn một bảng để làm mẫu cho các files, cuối cùng ta có kết quả như sau:

{{< figure src="./get-folder3.png" width=100% >}}

Các bạn chọn _Close & Load to_ để lưu lại kết quả.

### 2.3. Nhập dữ liệu từ website

Để nhập dữ liệu từ website, ta chọn _Get From Web_ và nhập đường link của trang web cần lấy dữ liệu: [Federal Reserve](https://www.federalreserve.gov/releases/h10/Hist/dat00_ca.htm)

{{< figure src="./get-from-web.png" width=80% >}}

### 2.4. Một số thao tác với Power Query

- Xóa các cột không cần thiết.
- Lọc dữ liệu.
- Đổi tên cột.
- Xác định kiểu dữ liệu của từng cột.
- Thêm cột.
- Append và merge.
- Biến đổi và làm sạch dữ liệu.
- Pivot và unpivot.
