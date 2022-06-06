---
title: "Lướt nhanh qua Excel"
subtitle: ""
slug: excel-notes
date: 2020-12-25
lastmod: 2020-12-25
draft: false
authors: ["Tuyen Kieu"]
images: ["featured.png"]
tags: ["Excel"]
categories: []
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

## 1. Data validation

Data validation được sử dụng để:

- Hạn chế dữ liệu nhập vào trong một ô bằng các tiêu chí.
- Đưa ra các cảnh báo nếu dữ liệu nhập sai.
- Đưa ra gợi ý về dữ liệu cần nhập.
- Data validation sẽ bị hủy nếu người dùng paste dữ liệu vào ô.

## 2. What-If analysis

**Scenario Manager**: Tạo ra các kịch bản và với mỗi kịch bản sẽ có một cột input ảnh hưởng đến output.

**Data Table**: Cho phép chúng ta xem sự thay đổi giá trị trong một ô output với các giá trị khác nhau của một hoặc hai ô input được xác định.

{{< figure src="what-if2.png" width=70% >}}

**Goal Seek**: Giải phương trình, giả sử ta có một output xác định và ta cần đi tìm input tương ứng.

## 3. Text to columns

Text-to-columns được sử dụng để phân tách dữ liệu trong một cột thành nhiều cột khác nhau dựa vào các ký tự đặc biệt như dấu `,` hoặc tab,...hoặc độ dài cố định của các ký tự.

## 4. Flash fill

Flash Fill cho phép chúng ta tách dữ liệu trong một cột thành nhiều cột khác nhau, dựa vào pattern trong hàng đầu tiên. Nó không dựa vào công thức nên có đôi khi sẽ không chính xác với những gì chúng ta mong muốn.

{{< figure src="flash-fill.jpg" width=70% >}}

## 5. Các hàm hay sử dụng

- Hàm tổng hợp dữ liệu: _SUM(), COUNT(), MIN(), MAX(), AGGREGATE(), SUBTOTAL()_
- Hàm Logic: _AND(), OR(), NOT(), IF()_
- Hàm thống kê: _AVERAGE(), MEDIAN(), MODE(), STDEV()_
- Hàm điều kiện: _SUMIF(), COUNTIF(), AVERAGEIF()_
- Hàm text: _UPPER(), LOWER(), PROPER(), LEFT(), RIGHT(), MID()_
- Hàm nối: _CONCATENATE()_
- Hàm thời gian: _NOW(), TODAY(), DATE(), TIME()_
- Hàm tham chiếu: _VLOOKUP(), INDEX(array, row, col), MATCH(lookup_value, array, type), INDIRECT()_

## 6. Quick analysis

**Quick analysis:** là một tính năng đưa ra một số gợi ý giúp chúng ta thực hiện các phân tích dữ liệu một cách nhanh chóng.

{{< figure src="quick-analysis-tool.png" width=70% >}}

## 7. Subtotals

**Subtotals:** là một tính năng tổng hợp dữ liệu theo từng giá trị định tính trong một cột xác định.

{{< figure src="subtotals-excel.png" width=40% >}}

## 8. Tables

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

## 9. Làm việc với mảng

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

## 10. Một số tính năng khác

- Sort and Filter
- Conditional Formatting
- Chart
- PivotTable
- PivotChart
- Shapes
