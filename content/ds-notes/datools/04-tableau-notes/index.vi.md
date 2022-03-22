---
title: "DA Tools - Tableau notes"
subtitle: ""
slug: tableau-notes
date: 2022-02-27
lastmod: 2022-02-27
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["DA Tools"]
categories: []
series: [Data Analysis Tools]
series_weight: 4
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

## 1. Làm quen với Tableau

Tableau là một phần mềm hỗ trợ phân tích và trực quan hóa dữ liệu *(Data Visualization)*, và thường được sử dụng ở trong ngành Business Intelligence (BI).

Trước khi bắt đầu, ta cần cài đặt [Tableau Public](https://public.tableau.com/en-us/s/). Sau đó, khởi động lên ta có màn hình *start page* như sau:

{{< figure src="tb-start-page.png" >}}

Như chúng ta thấy thì, ở giao diện đầu tiên Tableau gồm 3 phần:

- Connect: Thông tin về các nguồn dữ liệu mà Tableau có thể đọc.
- Open: Danh sách các Project mà chúng ta đã và đang làm việc.
- Discover: Thông tin về các nguồn tài liệu mã nguồn mở như training, resources.

### 1.1. Connect

Ở phần Connect, ta click vào *Microsoft Excel*, Tableau sẽ đưa ta đến nơi chứa tập dữ liệu mẫu kèm theo khi cài đặt. Nó có tên là `Sample - Superstore.xls`. 

{{< figure src="superstore.png" >}}

Sau đó ta kéo Sheet Orders vào khu vực *Drag sheets here*, ta có kết quả như sau:

{{< figure src="connect.png" >}}

### 1.2. Tableau Workspace

Chúng ta click vào *Sheet 1* ở góc dưới màn hình, để vào không gian làm việc chính của Tableau:

{{< figure src="workspace.png" >}}

### 1.3. Measures và Dimensions

Khi kết nối đến một nguồn dữ liệu, theo mặc định Tableau sẽ dựa vào kiểu dữ liệu của một cột (biến, trường) để phân loại vào một trong hai loại:

- Measures: sẽ chứa các con số, giá trị liên tục hoặc giá trị định tính mà có thể đo được. Measures thường đi kèm với màu xanh lá.
- Dimensions: thì sẽ chứa các giá trị định tính, ví dụ như dữ liệu họ tên, ngày tháng, dữ liệu địa lý,...Dimensions thường đi kèm với màu xanh dương.

{{< admonition type=notes title="Lưu ý" open=true >}}
Nếu Tableau nhận diện sai các biến khi phân loại vào Measures hoặc Dimensions thì chúng ta có thể chỉnh sửa lại bằng cách kéo thả.
{{< /admonition >}}

### 1.4. Vẽ thử một biểu đồ

Ta kéo biến *Sales* vào ô Rows, biến *Category* vào ô Columns. Tiếp theo, ta sẽ kéo biến *Segment* vào ô Color và biến *Profit* vào ô Tooltip để thêm chú thích. 

Tada, và đây là kết quả chúng ta, khá là xấu:

{{< figure src="first-chart.png" >}}

Cuối cùng, để kết thúc công việc, chúng ta vào File và chọn Save để lưu kết quả.

## 2. Import data
