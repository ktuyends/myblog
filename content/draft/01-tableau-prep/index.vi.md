---
title: "DA Tools - Tableau Prep (Phần 1)"
subtitle: ""
slug: tableau-prep
date: 2021-12-16
lastmod: 2021-12-16
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Tableau"]
categories: []
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

## 1. Giới thiệu Tableau Prep

{{< youtube 1tpgs5hCr2o >}}

### 1.1. Làm quen với Tableau Prep

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

### 1.2. Lập kế hoạch chuẩn bị dữ liệu

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

### 1.3. Shaping Data

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

### 1.4. Các kiểu dữ liệu trong Tableau

**Numbers:**

Số (numbers) trong Tableau gồm hai loại:

- Số nguyên
- Số thực

Một số hàm sử dụng với dữ liệu số:

- Làm tròn: *round(), ceiling(), floor()*
- Giá trị tuyệt đối: *abs()*
- Zero is null: *zn()*
- Hàm *sign()*: Trả về -1 nếu âm, 1 nếu dương, còn lại trả về 0.

> Tableau Prep không phân biệt các ký tự in hoa với in thường

**Dates:**

Một số hàm sử dụng với Date:

- Hàm *dateadd()*
- Hàm *makedate()*
- Hàm *dateparse()*

**String:**

Một số thuộc tính của string (chuỗi các ký tự):

- Mỗi ký tự có một vị trí (Bao gồm khoảng trắng, ký tự đặc biệt)
- Các ký tự có thể được sắp xếp từ *A -> Z*
- Các ký tự có thể phân biệt giữa in hoa với in thường
- Đôi khi cần chia tách các ký tự, ví dụ như giữa họ và tên
- Sự đồng nhất, ví dụ quá khứ sử dụng một tên khác, hiện tại sử dụng một tên khác. Ví dụ City và city có sự khác nhau về chính tả
- Khoảng trắng, đôi khi hai giá trị nhìn có vẻ giống nhau nhưng lại không khớp, đó có thể là do khoảng trắng giữa hai giá trị khác nhau

Một số hàm hay sử dụng với string:

- Hàm *split()*: Tách một chuỗi ký tự dài thành các chuỗi ngắn hơn
- Hàm *trim()*: Loại bỏ các khoảng trắng thừa
- Hàm *upper()* và *lower()*: Chuyển đổi ký tự thành in hoa hoặc in thường
- Hàm *left()*, *right()*, *mid()*: Trích xuất ký tự dựa vào vị trí
- Hàm *find()*, *findnth()*: Xác định vị trí xuất hiện của ký tự
- Hàm *len()*: Trả về độ dài của một chuỗi ký tự
- Hàm *replace()*: Thay thế các ký tự

**Một số hàm liên quan đến kiểu Boolean**

Hàm IFF: Kiểm tra dựa trên điều kiện logic

```
IIF(logical test, if True return this, if False return this)
```

Hàm *contains()*: Kiểm tra xem một chuỗi ký tự có nằm trong một chuỗi không

```
contains([columns],'keyword')
```

Hàm *IsDate()*, *IsNull()*

Hàm *IF/THEN*, cấu trúc 1:

```
IF <logical test> THEN <if True return this>
ELSE <if False return this>
end
```

Cấu trúc 2:

```
IF <logical test 1> THEN <if True return this 1>
ELSEIF <logical test 2> THEN <if True return this 2>
...
ELSE <if False return this>
end
```


Hàm *CASE*: Kiểm tra dựa trên giá trị

```
CASE [Columns]
WHEN <value 1> THEN <return this 1>
WHEN <value 2> THEN <return this 2>
...
END
```

## 2. Shape of Data

## 3. Output
