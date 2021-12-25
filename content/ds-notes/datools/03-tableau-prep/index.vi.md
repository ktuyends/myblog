---
title: "DA Tools - Tableau Prep"
subtitle: ""
slug: tableau-prep
date: 2021-12-16
lastmod: 2021-12-16
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["DA Tools"]
categories: []
series: [Data Analysis Tools]
series_weight: 3
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

## 1. Làm quen với Tableau Prep

**Cài đặt Tableau Prep Builder**

Đầu tiên, chúng ta cần cài đặt [Tableau Prep Builder](https://www.tableau.com/support/releases/prep). Sau khi cài đặt, ta có giao diện như sau:

{{< figure src="tableau-prep.png" >}}

- Connections: Danh sách các kết nối được hỗ trợ
- Recent Flows: Chứa các flow chúng ta đang tạo
- Sample Flows: Một số flow mẫu từ Tableau team
- Discover pane: Các tutorial trên blog của Tableau

**Một số bước chuẩn bị dữ liệu cơ bản**

Bước 1: Input Data

Sau khi kết nối với data source, chúng ta sẽ kéo các bảng dữ liệu từ Connections vào Canvas (vùng giữa màn hình)

{{< figure src="tb-prep-02.png" >}}

- Flow Pane: Các bước chuẩn bị dữ liệu
- Input Pane: Vùng màu xám, nơi thiết lập về các files
- Data Fields: Chọn dữ liệu để đưa vào quy trình 

Bước 2: Clean Step

Sau khi đã chọn được dữ liệu, ta click chuột vào dấu *+* trong Flow Pane.

{{< figure src="tb-clean.png" >}}

Bước 3: Output Step

{{< figure src="tb-output.png" >}}


Đây là bước cuối cùng, sau khi dữ liệu đã được xử lý xong. 

> Lưu ý: Trong quá trình xử lý dữ liệu, chúng ta nên thường xuyên lưu lại kết quả của mình. Tableau Prep có hai định dạng đầu ra:
> - Tableau flow file (.tfl): Chỉ lưu logic của flow và vị trí của input, output.
> - Packaged Tableau flow file (.tflx): Lưu mọi thứ, bao gồm flow, các files input và output.

## 2. Lập kế hoạch chuẩn bị dữ liệu

**Bước 1: Hiểu về dữ liệu**

- Cấu trúc của bảng dữ liệu: Dữ liệu gồm bao nhiêu cột, bao nhiêu hàng, mỗi cột có định dạng gì?
- Tên của các cột dữ liệu có chính xác không?
- Kiểu dữ liệu trong mỗi cột: Mỗi cột chỉ nên có một kiểu dữ liệu ví dụ như number, text, date time, boolean
- Mỗi hàng đại diện cho điều gì?
- Dữ liệu có giá trị thiếu không (Missing Value)?
- Dữ liệu có giá trị ngoại lai, giá trị sai không?

**Bước 2: Xác định trạng thái dữ liệu mong muốn**

Với Columns:

- Có quá nhiều cột không, loại bỏ các cột không cần thiết hoặc sử dụng Pivot để gom các hàng tương tự thành một cột
- Có cột nào bị thiếu không, sử dụng Join để thêm các cột cần thiết
- Tên cột có rõ ràng không, nếu không hãy sửa đổi lại
- Calculations: Tạo ra các cột mới, dựa trên các cột đã có

Với Rows:

- Có nhiều hàng hơn dữ kiến không, loại bỏ các hàng không cần thiết
- Có ít hàng hơn dữ kiến không, thêm các hàng bằng Union
- Các giá trị có bị sai không, có bị thiếu không, có khoảng trắng thừa không...

**Bước 3: Xây dựng Flow**

## 3. Shaping Data

Shaping data chúng ta có thể hiểu đơn giản là thay đổi cấu trúc bảng dữ liệu bằng phép xoay. Ví dụ có thể chuyển một cột thành nhiều cột, hoặc chuyển nhiều cột thành một cột.

{{< figure src="reshaping-data.gif" >}}

Khi Shaping data, ta cần chú ý 3 điểm sau:

- Mỗi trường dữ liệu được đại diện bởi một cột hay nhiều cột
- Trường dữ liệu thuộc dạng Dimensions (Dữ liệu định tính) hay Measures (Dữ liệu định lượng)
- Mỗi trường dữ liệu có phải có một kiểu dữ liệu duy nhất không? Measures thường yêu cầu dữ liệu có kiểu số nguyên hoặc số thực.

Một số cách Shaping data chúng ta có thể làm với Tableau:

- Pivot 1, Columns to rows
- Pivot 2, Rows to columns
- Aggregate
- Join
- Union
