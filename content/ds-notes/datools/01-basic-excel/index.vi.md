---
title: "DA Tools - Lướt qua Excel"
subtitle: ""
slug: basic-excel
date: 2021-12-14
lastmod: 2021-12-14
draft: false
authors: ["Tuyen Kieu"]
description: "Excel là một trong những công cụ linh hoạt, dễ học và được sử dụng phổ biến nhất trong Data Analysis."
images: []
tags: ["DA Tools"]
categories: []
series: [Data Analysis Tools]
series_weight: 1
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

Excel là một trong những công cụ linh hoạt, dễ học và được sử dụng phổ biến nhất trong Data Analysis. Với sự bùng nổ về dữ liệu và sự phát triển mạnh mẽ của các công cụ xử lý dữ liệu, Excel cũng đã thêm nhiều tính năng và công cụ mới để hỗ trợ phân tích dữ liệu tốt hơn. 

Trong bài viết này, tôi không viết về cách sử dụng Excel, tôi chỉ đơn giản là đi lướt qua một số tính năng của Excel mà thôi.

## 1. Các kiến thức cơ bản cần biết

- Sort and Filter
- conditional Formatting
- Data Validation
- Chart
- Functions: IFERROR(), IF(), AND(), OR()
- Các toán tử: >, >=, <, <=, =, <>
- Functions: SUBTOTAL(), SUMIFS(), COUNTIFS(), COUNT + COUNT (OR)
- Functions: VLOOKUP(), HLOOKUP(), INDEX(), MATCH()
- Table, Range Names
- PivotTable and Pivot Chart, Slicers
- Power Query, Power Pivot

## 2. Một số ghi chú

### Paste Special 

Phím tắt: Ctrl + Alt + V

{{< figure src="paste-special.png" >}}

- Ba kiểu Paste hay sử dụng: Formulas, Values, Formats
- Multiply: nhân giá trị bị Copy với ô được Paste
- Transpose: để chuyển vị một mảng

### Formula Auditing

{{< figure src="range-name.png" >}}

- Evaluate Formula: Đánh giá công thức theo từng bước
- Trace Precedents, Trace Dependents, Remove Arrows: Hiển thị các ô liên quan đến công thức hiện tại

### Range Name

Đặt tên cho một vùng, mảng nào đó để tiện cho việc tham chiếu. Chúng ta có một số lựa chọn như sau:

- Trong ô Name Box: Đặt tên cho một ô hoặc vùng được lựa chọn
- Sử dụng Define Name: Tương tự như Name Box
- Create from Selection: Đặt tên cho nhiều cột hoặc hàng được lựa chọn, mỗi cột hoặc hàng là một tên.

### Table

Tương tự như Range Name, nhưng Table có nhiều tính năng hơn, có thể tự động hóa nhiều thao tác xử lý dữ liệu, và dễ dàng tích hợp với các công cụ Power Tools. Để tạo một Table, chỉ cần chọn vùng dữ liệu cần tạo Table, sau đó chọn *Insert > Table*.

Tham chiếu khi sử dụng table:

- table_name: Tham chiếu đến bảng
- table_name[Column]: Tham chiếu đến cột
- table_name[@[Column]]: Tham chiếu đến hàng hiện tại

### Làm sạch dữ liệu

Một số hàm và tính năng được sử dụng trong làm sạch dữ liệu:

- Flash Fill
- Text to Column: Phân tách, chuyển đổi định dạng
- Remove Duplicate: Xóa các hàng trùng lặp
- PROPER(), LOWER(), UPPER()
- Spelling Check
- CLEAN(): Loại bỏ các ký tự lạ
- TRIM(): Loại bỏ khoảng trắng thừa
- SUBSTITUTE(): Thay thế các ký tự
- VALUE(): Chuyển dữ liệu dạng text thành dữ liệu dạng số
- RIGHT(), MID(), LEFT(), LEN(), FIND(), SEARCH(), CONCATENATE()

> Lưu ý khi làm sạch dữ liệu chúng ta không sửa trực tiếp dữ liệu gốc.

### Một số phím tắt hay dùng

- F2: Sửa ô hiện tại
- F4: Lock cell
- Ctrl + Shift + Arrow, Ctrl + Shift + End: Chọn nhiều dữ liệu

## 3. Power Query

{{< figure src="power-tools.png" >}}

Power Query là một tập hợp các công cụ mạnh mẽ cho phép chúng ta nhập dữ liệu từ nhiều nguồn khác sau vào trong Excel, sau đó thực hiện các thao tác biến đổi và làm sạch [^1]:

[^1]: Nguồn ảnh: https://www.howtoexcel.org/

{{< figure src="get-data.png" >}}

Một số nguồn dữ liệu phổ biến:

- Các excel files, excel tables
- Cơ sở dữ liệu SQL
- Một folder chứa các files

Chúng ta có thể gộp các files với nhau:

- Merge queries: Tương tự như Join trong SQL
- Append queries: Tương tự như Union trong SQL

### Quy trình làm việc với Power Query

**Bước 1:** Lấy dữ liệu từ các nguồn khác nhau: *Data > Get Data*

**Bước 2:** Một bảng Navigator xuất hiện: 

{{< figure src="get-data-2.png" >}}

Chúng ta chọn bảng dữ liệu muốn nhập và sau đó chọn Edit/Transform tùy phiên bản của các bạn để vào Query Editor:

{{< figure src="editor.png" >}}

Đây là nơi chúng ta thực hiện các thao tác xử lý, biến đổi và làm sạch dữ liệu:

- Ô số 3: Data Preview, có thể phóng to, thu nhỏ bằng phím tắt Ctrl + Shift + "+/-"
- Ô số 5: Tên của Query hiện tại
- Ô số 6: Các thao tác của chúng ta được ghi lại theo các bước
- Ô số 4: Formula Bar, sử dụng ngôn ngữ "M", tương ứng với các bước thao tác

{{< figure src="formula.png" >}}

**Bước 3:** Sau khi thực hiện các thao tác xử lý, biến đổi dữ liệu. Chúng ta cần lưu lại kết quả của mình: *File > Close and Load to*

{{< figure src="close.png" >}}

Ở đây, các bạn có thể lưu kết quả dưới dạng Table, hoặc nếu k muốn xuất kết quả thì ta chọn vào: *Only Create Connection*

**Bước cuối cùng:** Power Query không tự cập nhật lại kết quả khi chúng ta thay đổi dữ liệu nguồn, vì vậy chúng ta cần phải Refresh lại Outputs hoặc Queries tương ứng.

## 4.Power Pivot

Khi làm việc với Excel, ta phải gom rất rất nhiều tập dữ liệu vào một tập dữ liệu để phân tích và xử lý. Cách làm này, có thể hiệu quả với các tập dữ liệu nhỏ, nhưng khi dữ liệu của chúng ta trở nên rất nhiều và lớn. Excel sẽ không thể nào xử lý được. Power Pivot, là một công cụ giúp chúng ta giải quyết khó khăn này. 

Giả sử ta có rất nhiều các bảng dữ liệu (tập dữ liệu), có thể được lưu trữ ở một nơi hoặc nhiều nơi khác nhau, ví dụ như các bảng excel, database, web data,...Power Pivot giúp chúng ta liên kết các tập dữ liệu này với nhau nếu chúng có một mối quan hệ nhất định. Công việc của chúng ta đơn giản là xác định các mối quan hệ và sau đó liên kết các tập dữ liệu này lại với nhau. Ta gọi nó là Data Model, và coi nó như một tập dữ liệu lớn để phân tích mà không cần phải gộp tất cả vào một bảng. 

### Lookup Table và Data Table

Data Model là một khái niệm rất quan trọng khi làm việc với Power Pivot, Power BI. Tạm thời ta có thể hiểu Data Model là một tập hợp các bảng được kết nối với nhau thông qua các khóa tương tự như cơ sở dữ liệu quan hệ. Data Model thông thường sẽ gồm hai loại bảng: 

- Bảng data (hoặc bảng fact)
- Bảng lookup (hoặc bảng Dim, Dimension)

Data Table là cấp độ thông tin đầu tiên mà chúng ta nghĩ đến, thường ở dạng Number hoặc Value. Thông thường Data Table sẽ có các cột "key" hoặc "id" được sử dụng để tạo ra các liên kết.

Lookup Table thường ở dạng Text, được sử dụng để cung cấp các thông tin bổ sung, diễn giải cho các "key" trong Data Table.

{{< figure src="data-model.png" >}}

Ví dụ trong bảng này, bảng màu xanh dương sẽ là bảng Data, còn bảng màu cam và xanh lá sẽ là bảng Lookup bổ sung thông tin cho các key trong bảng màu xanh dương.

> Lưu ý: Một bảng, có thể là Lookup table cho bảng này nhưng lại là Data table của bảng khác.

### Thêm Add-ins Power Pivot

Đầu tiên, ta phải thêm Add-ins Power Pivot nếu nó chưa được thêm: *File -> Option -> Add-ins -> COM Add-ins -> Go*, sau đó tích vào Power Pivot và OK để hoàn thành.

Kết quả:

{{< figure src="power-pivot.png" >}}

Để vào cửa sổ Power Pivot, ta chọn *Manage Data Model*

{{< figure src="manage-pp.png" >}}

### Import và kết nối các bảng dữ liệu

Cách import các bảng dữ liệu rất đơn giản, giống như chúng ta import vào Power Query, nhưng lúc *Close and Load To...* ta chọn *Add this data to the Data Model* và *Only Create Connection*:

{{< figure src="close.png" >}}

Sau khi import các bảng dữ liệu, ta vào Power Pivot và Chọn *Diagram View* để bắt đầu thực hiện kết nối các bảng với nhau. Việc này khá đơn giản, ta chỉ cần kéo "key" từ data table vào lookup table.

> Lưu ý: Có một số cách sắp xếp các bảng, thường sẽ là các bảng lookup table ở trên cùng 1 hàng và data table ở phía dưới. Hoặc data table ở giữa còn lookup table ở xung quanh.

### Add Columns và Measures

Để thêm một Columns trong một bảng nào đó, ta click vào Add Columns và đặt tên cho cột đó. Sau đó nhập công thức trong ô formula giống như trong Excel.

Measures tương tự như những phép toán chúng ta đã gặp như SUM, COUNT. Tuy nhiên bằng việc sử dụng DAX, chúng ta có thể tạo ra các Measures phức tạp hơn. Để thêm Measures, trong tab Power Pivot ta chọn: *Measures -> New Measure*, sau đó nhập các thông tin cần thiết. 


> Lưu ý: Power Query sẽ sử dụng ngôn ngữ M, Power Pivot sử dụng ngôn ngữ DAX. Vì vậy các bạn sẽ cần phải tìm hiểu thêm về các công thức M và DAX. Công thức sử dụng DAX sẽ bắt đầu bằng dấu `=`.

### Sử dụng Pivot Table với Power Pivot

Sử dụng Pivot Table với Power Pivot tương tự như Pivot Table bình thường, chỉ khác việc chúng ta sẽ có nhiều bảng dữ liệu hơn:

- Trong Excel, chọn *Insert > PivotTable* hoặc
- Trong Power Pivot, chọn *PivotTable*

Sau đó chúng ta tích vào: *Use this workbook’s Data Model* và *Existing Workbook*.

Với Data Model, chúng ta hoàn toàn có thể tạo ra các Measures trực tiếp từ Pivot Table, bằng cách click chuột phải vào bảng muốn tạo Measures và chọn Add Measures.