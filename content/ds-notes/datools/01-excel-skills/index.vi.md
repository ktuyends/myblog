---
title: "DA Tools - Excel notes"
subtitle: ""
slug: excel-notes
date: 2022-02-24
lastmod: 2022-02-24
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["DA Tools"]
categories: []
series: [Data Analysis Tools]
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
- Hàm tham chiếu: _VLOOKUP(), INDEX(array, row, col), MATCH(lookup_value, array, type)_

### 1.6. Quick analysis

**Quick analysis:** là một tính năng đưa ra một số gợi ý giúp chúng ta thực hiện các phân tích dữ liệu một cách nhanh chóng.

{{< figure src="quick-analysis-tool.png" width=70% >}}

### 1.7. Subtotals

**Subtotals:** là một tính năng tổng hợp dữ liệu theo từng giá trị định tính trong một cột xác định.

{{< figure src="subtotals-excel.png" width=40% >}}

### 1.8. Tables

Tables trong Excel là một đối tượng đặc biệt được đặt tên và cho phép chúng ta quản lý nội dung bên trong một cách độc lập với phần còn lại của trang tính.

{{< figure src="tables.png" width=75% >}}

Một số cách tham chiếu đến dữ liệu trong Tables:

{{< figure src="tables-ref.png" width=75% >}}

### 1.9. Một số tính năng khác

- Sort and Filter
- Conditional Formatting
- Chart
- PivotTable
- PivotChart
- Shapes

## 2. Getting Data
