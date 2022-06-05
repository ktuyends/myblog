---
title: "Day 2 - Chuẩn bị dữ liệu"
subtitle: ""
slug: 02-data-preparation
date: 2022-05-24
lastmod: 2022-05-24
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["BI"]
categories: []
series: [BI Course Notes]
series_weight: 2
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

## 1. Getting data

Trước khi bắt đầu vào làm việc với dữ liệu, việc đầu tiên chúng ta cần phải làm là nạp dữ liệu _(import data)_ vào trong Power Query. Vì có rất nhiều nguồn cung cấp cấp dữ liệu, cho nên trong Power Query cũng có rất nhiều cách để _import data_ tương ứng với các nguồn khác nhau. Trong phần này, mình sẽ trình bày về một số nguồn cơ bản, phổ biến nhất.

### 1.1. From Tables

Nguồn dữ liệu đầu tiên là từ các Tables trong Excel, lưu ý Tables không phải là một bảng mà là một định dạng bảng trong Excel. Nếu bạn chưa biết Tables là gì thì mình nghĩ là các bạn nên tìm hiểu thêm về nó.

Để import data từ một Table vào Power Query, ta lựa chọn một ô bên trong Table sau đó ở trong file Excel đang mở vào _Data -> Get & Transfrom Data -> From Table/Range_

{{< figure src="./01-getting-data/Data-Import-Table-Range.png" width=75% >}}

Chúng ta có giao diện Power Query như sau:

{{< figure src="./01-getting-data/Power-Query-Interface-First-View.png" >}}

Trong đó:

- **Ribbon**: Tương tự như Excel, chứa một số thao tác chính được nhóm thành các nhóm riêng biệt.
- **Properties**: Nơi đặt tên cho các truy vấn.
- **Applied steps**: Giống như Macro trong Excel, mỗi một thao tác với dữ liệu sẽ được ghi thành một Step. Chúng ta có thể thêm hoặc chèn, sửa, xóa các Steps.
- **Data preview**: Đây là vùng hiển thị dữ liệu.

Lưu ý, nếu bạn để ý, thỉnh thoảng Power Query sẽ thêm một bước _Changed Type_ ngay phía sau các bước của chúng ta. Về cơ bản thì nó sẽ tự động xác định và thay đổi kiểu dữ liệu cho các cột. Nhưng việc này đôi lúc sẽ gây ra các lỗi không cần thiết. Mình nghĩ là nên tắt nó đi bằng cách vào _File -> Options and settings -> Options_, sau đó chọn Tab _Data Load_ ở mục **GLOBAL** và bỏ chọn tự động xác định kiểu ở _Type Detection_:

{{< figure src="./01-getting-data/type-detection.png" width=75% >}}

Các bạn có thể thực hiện một số thao tác và xem các thay đổi, đừng lo lắng về những gì sẽ xảy ra. Bước cuối cùng, sau khi _import data_ và thực hiện một số biến đổi, ta vào _Home -> Close and Load_ để lưu các thay đổi và load dữ liệu trở lại Excel, hoặc với Power BI thì sẽ thêm dữ liệu vào Data Model mà ta sẽ đi tìm hiểu các trong một bài viết khác.

### 1.2. From Text/CSV

Nguồn dữ liệu tiếp theo chúng ta muốn tìm hiểu là các file `.CSV` và file `.TXT`, các bước cũng tương tự như với Tables, ta sẽ vào _Data -> Get & Transfrom Data -> From Text/CSV_:

{{< figure src="./01-getting-data/Power-Query-CSV-Import.png" width=80% >}}

Sau khi chọn file cần import, ta có kết quả như sau:

{{< figure src="./01-getting-data/CSV-Load-or-Transform-data.png" width=80% >}}

Trong đó:

- **File Origin**: Là kiểu định dạng của file.
- **Delimiter**: Ký tự được sử dụng để ngăn cách các cột trong file.
- **Data Type Detection**: Số dòng được sử dụng để xác định kiểu dữ liệu của các cột.

Cuối cùng, ta bấm vào _Transform Data_ để import dữ liệu.

### 1.3. From Worksheet

Tương tự như hai phần trên, để import dữ liệu từ Worksheet ta vào _Data -> Get & Transfrom Data -> From File -> From Workbook_:

{{< figure src="./01-getting-data/Power-Query-Excel-File-Import.png" width=80% >}}

Sau khi chọn được file cần import, một giao diện mới được hiện lên, bạn click vào các sheet muốn import, như trong ví dụ này ta tạm thời chỉ import một sheet là _January_. Cuối cùng, click vào _Transform Data_ để import dữ liệu vào Power Query.

{{< figure src="./01-getting-data/Power-Query-Excel-File-Select-Worksheet.png" width=80% >}}

### 1.4. From Web

Web là một nơi rộng lớn với rất nhiều thông tin và dữ liệu, nhưng vì lưu trữ trên web nên không phải lúc nào chúng ta cũng lấy được dữ liệu hoặc cho dù có lấy được thì chúng ta cũng phải tra rất nhiều bước phức tạp. Trong phần này, chúng ta sẽ sử dụng Power Query để lấy dữ liệu từ trang web:

```
https://www.xe.com/currencytables/?from=USD&date=2019-07-01
```

Ta vào _Data -> Get & Transfrom Data -> From Web_, sau đó nhập đường link trên và chọn _Connect:_

{{< figure src="./01-getting-data/Get-data-form-the-Web.png" width=80% >}}

{{< figure src="./01-getting-data/Get-data-form-the-Web2.png" width=80% >}}

Power Query sẽ lấy rất nhiều bảng khác nhau từ trên Web, vì vậy ta cần xem lướt qua từng bảng để chọn được bảng dữ liệu mong muốn. Cuối cùng, click vào _Transform Data_ để import dữ liệu vào Power Query.

{{< figure src="./01-getting-data/Get-data-form-the-Web3.png" width=80% >}}

{{< admonition type=notes title="Thay đổi vị trí tập dữ liệu" open=false >}}

Đôi lúc, khi bạn gửi một file Power BI từ máy này qua máy khác, có thể sẽ gặp một số vấn đề khi vị trí của tập dữ liệu ở máy tính ban đầu không giống với máy tính được gửi đến. Khi đó, ta cần phải thay đổi lại vị trí của tập dữ liệu để các queries hoạt động lại bình thường. Có một vài cách để làm điều này:

**Thay đổi trực tiếp ở query Source**

{{< figure src="./01-getting-data/Change-Source-Formula-Bar.png" width=80% >}}

**Thay đổi ở Advanced Editor**

{{< figure src="./01-getting-data/Change-Source-Advanced-Editor.png" width=80% >}}

**Thay đổi khi click vào option ở query Source**

{{< figure src="./01-getting-data/Change-Source-Gear-Icon.png" width=80% >}}

**Cách cuối cùng, thay đổi ở Data Source Settings**

{{< figure src="./01-getting-data/Home-Data-Source-settings.png" width=80% >}}

{{< figure src="./01-getting-data/Data-source-settings-window.png" width=80% >}}

{{< /admonition >}}

### 1.5. Close and Load

Phần này chủ yếu sẽ áp dụng trên Excel, vì trong Power BI khi ta click vào Load nó sẽ thêm tập dữ liệu vào trong Data Model.

{{< figure src="./01-getting-data/Home-Close-and-Load-To.png" width=40% >}}

Khi bạn click vào _Close and Load To_, một cửa sổ với các tùy chọn hiện ra:

{{< figure src="./01-getting-data/Import-Data-Window.png" width=40% >}}

Ở đây, chúng ta có bốn lựa chọn:

- **Table**: Tạo ra một bảng mới trong một Sheet của Excel.
- **PivotTable**: Thêm bảng dữ liệu vào PivotTable.
- **PivotChart**: Tương tự như PivotTable.
- **Only Create Connection**: Chỉ tạo các kết nối, output không được hiển thị ở bất kỳ đâu ngoại trừ Power Query. Tuy nhiên, nó có thể được sử dụng trong các queries khác hoặc là như một tham số _(parameters - chúng ta sẽ tìm hiểu ở bên dưới)_.

### 1.6. Data Refresh

Không giống với các công thức trong Excel, theo mặc định các phép tính sẽ thay đổi khi dữ liệu bị thay đổi. Power Query chỉ thực hiện tính toán lại khi chúng ta yêu cầu nó:

{{< figure src="./01-getting-data/Data-Refresh-All.png" width=80% >}}

Ở đây, chúng ta có ba lựa chọn cơ bản:

- **Refresh All**: Cập nhật tất cả các queries trong tất cả các Tables.
- **Refresh**: Chỉ cập nhật dữ liệu trong Tables hiện tại.
- **Connection Properties**: Trong này sẽ có một số tùy chọn về tự động cập nhật dữ liệu.

Lưu ý, nếu Power Query lấy dữ liệu từ các files bên ngoài, nó chỉ cập nhật với các dữ liệu bị thay đổi được lưu. Tuy nhiên, nếu các Tables ở trong cùng một Workbook sử dụng Power Query thì nó được cập nhật ngay cả khi ta chưa lưu.

## 2. Data transformations

Phần này, chúng ta sẽ đi lướt nhanh qua một số thao tác biến đổi dữ liệu được xây dựng sẵn trong thanh Ribbon của Power Query. Nội dung mình tổng hợp từ một số bài viết trong series của [Excel Off The Grid](https://exceloffthegrid.com/power-query-basic-transformations/) và một số video trên Channel [My Online Training Hub](https://www.youtube.com/playlist?list=PLmd91OWgLVSKnVrL0YxdOH61MAiqlFHac).

### 2.1. Home Tab

{{< figure src="./02-transformation/Manage-Columns-Section.png"  >}}

**Manage Columns**: Chứa một số tùy chọn làm giảm số cột không cần thiết.

- _Choose Columns:_ Chọn các cột để giữ lại trong phần _Preview_, xóa các cột còn lại.
- _Go To Column:_ Chọn một cột cụ thể.
- _Remove Columns:_ Xóa các cột được lựa chọn.
- _Remove Other Columns:_ Xóa các cột không được lựa chọn.

{{< figure src="./02-transformation/Reduce-Rows-Section.png" >}}

**Reduce Rows**: Chứa một số tùy chọn làm giảm các dòng không cần thiết.

- _Keep Top Rows_: Giữ lại m dòng đầu tiên, m là số dòng bạn nhập vào khi cửa sổ hiện lên.
- _Keep Bottom Rows_: Giữ lại m dòng cuối cùng.
- _Keep Range of Rows_: Giữ lại n dòng tính từ dòng thứ m.
- _Remove Top Rows_: Xóa m dòng đầu tiên.
- _Remove Bottom Rows_: Xóa m dòng cuối cùng.
- _Remove Alternate Rows_: Xóa m dòng, giữ lại n dòng, sau đó lặp lại quy luật trên.
- _Keep Duplicates_: Lấy ra các giá trị bị lặp lại.
- _Keep Errors_: Lấy ra các giá trị bị lỗi.
- _Remove Duplicates_: Xóa các dòng bị lặp lại, chỉ giữ lại dòng đầu tiên.
- _Remove Blank Rows_: Xóa các dòng trống.
- _Remove Errors_: Xóa các dòng có giá trị lỗi.

### 2.2. Transform Tab

{{< figure src="./02-transformation/use-first-row-as-headers.png" >}}

**Group By**: Tổng hợp dữ liệu.

**Use First Row as Headers**: Sử dụng hàng đầu tiên làm tên cột.

**Use Headers as First Row**: Chuyển tên cột thành hàng đầu tiên trong bảng dữ liệu.

**Transpose**: Chuyển vị.

**Reverse Rows**: Sắp xếp các dòng theo thứ tự ngược lại.

**Count Rows**: Đếm số dòng dữ liệu.

{{< figure src="./02-transformation/Any-Column-Section.png" >}}

**Data Type**: Chuyển đổi kiểu dữ liệu của cột hiện tại.

**Detect Data Type**: Xác định và đổi kiểu dữ liệu của những cột được lựa chọn. Có thể sử dụng tùy chọn `Ctrl + A` để chọn toàn bộ các cột sau đó sử dụng tùy chọn này để đổi kiểu dữ liệu.

**Rename**: Đổi tên cột (biến, thuộc tính) của cột hiện tại.

**Replace Values**: Thay thế một giá trị cũ bằng giá trị mới trong một cột.

**Replace Errors**: Tương tự như _Replace Values_, nhưng giá trị bị thay thế là các giá trị lỗi.

**Fill Up / Down**: Lấp đầy các giá trị trong các ô missing values bằng giá trị của ô bên trên hoặc bên dưới trong cùng một cột.

**Move**: Di chuyển vị trí của các cột dữ liệu.

**Pivot Column**: Hoặc là tương tự như PivotTable trong Excel, hoặc là chuyển đổi định dạng bảng từ stacked sang unstacked.

**Unpivot Columns**: Chuyển đổi định dạng bảng từ unstacked sang stacked.

{{< figure src="./02-transformation/Text-Column-Section.png" >}}

**Split Column:** Tách một cột thành nhiều cột dựa vào một số đặc điểm nhận biết.

**Format:** Một số thao tác chuyển đổi các ký tự, loại bỏ khoảng trắng,...

**Merge Columns:** Gộp hai cột thành một cột.

**Extract:** Tạo ra một cột mới, với các giá trị là một chuỗi con được xác định dựa trên một pattern nào đó của cột ban đầu.

{{< figure src="./02-transformation/Number-Column-Section.png" >}}

**Statistics**: Một số thông tin thống kê mô tả.

**Standard**: Một số phép toán cộng, trừ, nhân, chia thêm một giá trị vào một cột.

**Rounding**: Làm tròn số.

**Information**: Kiểm tra xem một giá trị ở dạng chẵn, lẻ, âm, dương hay giá trị $0$.

**Scientific and Trigonometry**: Một số hàm giải tích và lượng giác.

{{< figure src="./02-transformation/Date-Time-Column.png" >}}

**Date & Time Column**: chứa một số lựa chọn xử lý kiểu dữ liệu _date, time, datetime_.

### 2.3. Custom Column

Hầu hết các thao tác biến đổi và xử lý dữ liệu cơ bản đã được Power Query hỗ trợ. Nhưng đôi khi, có những vấn đề khó, đòi hỏi chúng ta phải tạo ra những cột mới để xử lý. Khi đó ta sẽ sử dụng _Custom Column_. Lưu ý Power Query sử dụng ngôn ngữ M, nên các hàm đôi khi sẽ không giống với Excel.

Được rồi, để bắt đầu tạo một cột mới ta vào _Add Column -> Custom Column_

{{< figure src="./02-transformation/Custom-Column-Window.png" width=70% >}}

Nhìn vào hình, ta có một số khu vực như:

1. **New column name**: Tên của cột mới được tạo ra.
2. **Available columns**: Tên của các cột trong bảng dữ liệu hiện tại.
3. **Formula**: Biểu thức tính toán.
4. **Error check**: Kiểm tra xem biểu thức có bị lỗi hay không.

**Một số phép toán cơ bản**

```
= [Column 1] + [Column 2]       // Phép cộng
= [Column 1] - [Column 2]       // Phép trừ
= [Column 1] * [Column 2]       // Phép nhân
= [Column 1] / [Column 2]       // Phép chia
= [Column 1] & [Column 2]       // Phép nối
= Number.Power(number, power)   // Số mũ
= [Column 1] = [Column 2]       // So sánh ngang bằng
```

**Hàm chuyển đổi kiểu dữ liệu**

- _Text.From_ – Chuyển đổi kiểu dữ liệu thành kiểu text.
- _Date.From_ – Chuyển đổi kiểu dữ liệu thành kiểu date.
- _Number.From_ – Chuyển đổi kiểu dữ liệu thành kiểu number.
- _Logical.From_ – Chuyển đổi các số thành `True` hoặc `False`.
- _Date.ToText_ – Chuyển đổi kiểu dữ liệu date thành kiểu text.
- _Date.FromText_ – Chuyển đổi kiểu dữ liệu text thành kiểu date.
- _Number.ToText_ – Chuyển đổi kiểu dữ liệu number thành kiểu text.
- _Number.FromText_ – Chuyển đổi kiểu dữ liệu text thành number.
- _Logical.FromText_ – Chuyển đổi giá trị `True` hoặc `False` ở dạng text thành Boolean.
- _Logical.ToText_ – Ngược lại với _Logical.FromText_.

**Lưu ý**: các công thức áp dụng cho từng hàng trong bảng dữ liệu, M áp dụng chỉ số bắt đầu là `0` và phân biệt giữa ký tự in hoa và in thường.

### 2.4. Conditional Column

Với _Conditional Column_, chúng ta có thể sử dụng các điều kiện trong biểu thức của mình để tạo ra các giá trị mới.

{{< figure src="./02-transformation/Add-Column-Conditional-Column.png" width=70% >}}

{{< figure src="./02-transformation/Conditional-Column-with-settings.png" width=70% >}}

Ngoài ra ta có thể sử dụng M Code bên trong _Custom Column_:

```
if <dieu_kien> then <gia_tri>
else if <dieu_kien> then <gia_tri>
...
else <gia_tri>
```

Trong trường hợp bạn muốn kết hợp nhiều điều kiện, có thể sử dụng `and/or/not`.

Bây giờ, giả sử biểu thức của chúng ta trả về lỗi trên một số dòng và ta muốn thay thế giá trị lỗi này bởi một giá trị nào đó, thì ta có thể sử dụng mệnh đề `try...otherwise`:

```
try <biểu thức> otherwise <giá trị thay thế nếu biểu thức trả về lỗi>
```

### 2.5. Parameters

Giả sử, ta có một bảng như sau:

{{< figure src="./02-transformation/parameters.png" width=70% >}}

Bây giờ, chúng ta sẽ chọn _Keep Top Rows_ để lấy 2 dòng đầu tiên trong bảng:

{{< figure src="./02-transformation/parameters2.png" width=70% >}}

Như bạn thấy, có một công thức M Code như này:

```
= Table.FirstN(Source,2)
```

Power Query đã sử dụng một hàm được gọi là `Table.FirstN` với hai tham số:

- _Table_: Tên của bảng hoặc truy vấn tương ứng.
- _countOrCondition_: Số dòng mà bạn muốn lấy, trong ví dụ trên là 2.

Bạn cũng có thể xem thông tin về một hàm bằng cách nhập tên hàm trong ô formula:

{{< figure src="./02-transformation/parameters3.png" width=100% >}}

Quay lại với nội dung của phần này, chúng ta hoàn toàn có thể thay thế giá trị `2` ở trên bằng một tham số mà khi ta thay đổi giá trị của tham số thì truy vấn cũng thay đổi theo.

Để tạo một tham số, ta vào _Manage Parameters -> New Parameter_, nhập tên tham số và các giá trị tương ứng, sau đó click vào OK để hoàn tất.

{{< figure src="./02-transformation/parameters4.png" width=60% >}}

Đến đây, bạn có thể thay tham số vào trong hàm `Table.FirstN` như sau:

```
= Table.FirstN(Source, Parameter1)
```

Bạn thử thay đổi giá trị của tham số, sau đó quay trở lại query để xem kết quả.

Trên thực tế, ta cũng có thể sử dụng Query như một tham số nếu query đó có kiểu dữ liệu tương ứng với kiểu dữ liệu của tham số trong hàm. Ví dụ, mình click chuột phải vào một ô và chọn _Drill Down_ để lấy ra giá trị bên trong ô đó.

{{< figure src="./02-transformation/parameters5.png" width=70% >}}

Bây giờ, ta thay đổi tên của Query vào trong hàm `Table.FirstN`

```
= Table.FirstN(Source, Query_Param)
```

### 2.6. Custom Funtion

Giả sử chúng ta có 3 file dữ liệu như sau:

{{< figure src="./02-transformation/custom-function.png" width=90% >}}

Đây là dữ liệu bán hàng theo từng tháng, dĩ nhiên là bên trong các file có cấu trúc giống nhau nhưng sẽ khác nhau về mặt giá trị. Bây giờ chúng ta muốn viết một hàm với input là tên của tập dữ liệu và output là một bảng dữ liệu đã được xử lý. Khi đó, thay vì phải xử lý từng tập dữ liệu, chúng ta chỉ cần áp dụng hàm này với tập dữ liệu mà ta muốn xử lý là xong.

{{< figure src="./02-transformation/custom-function2.png" width=80% >}}

Trước khi đi tạo một hàm, chúng ta cần import một tập liệu để làm mẫu và thực hiện các thao tác biến đổi để có được một tập dữ liệu tốt:

{{< figure src="./02-transformation/custom-function3.png" width=90% >}}

Có hai cách để tạo một function trong Power Query.

**Cách thứ nhất**: ta sẽ tạo một query duplicate của query và đặt tên nó là `ManualFunc`, sau đó bật _Advanced Editor_ lên để chỉnh sửa M Code:

{{< image src="./02-transformation/custom-function4.png" width=100% >}}

Như các bạn thấy, ta cần tạo một hàm, với một tham số thay thế cho đường link dẫn đến tên tệp mà mình đã bôi đậm trong hình. Cú pháp để tạo một hàm:

```
(Variable as Data Type, Variable as Data Type) as Data Type =>

(Output Expression)
```

Bây giờ, ta sửa lại đoạn M code và click vào OK để hoàn tất:

{{< image src="./02-transformation/custom-function5.png" width=100% >}}

Kết quả:

{{< figure src="./02-transformation/custom-function6.png" width=50% >}}

Bây giờ, ta sẽ áp dụng hàm này cho từng bảng một. Đầu tiên ta import folder chứa cả 3 file dữ liệu:

{{< figure src="./02-transformation/custom-function7.png" width=70% >}}

Tiếp theo, ta vào _Add Column -> Invoke Custom Function_ để tạo cột dữ liệu mới:

{{< figure src="./02-transformation/custom-function8.png" width=70% >}}

**Cách thứ hai:** Chúng ta sẽ xây dựng một function bắt đầu từ đây:

{{< figure src="./02-transformation/custom-function7.png" width=70% >}}

**Bước 1:** Ta cần chọn một file để làm mẫu bằng cách click chuột phải vào file đó và chọn _As a New Query_ và đổi tên query mới tạo thành _Sample File Binary_:

{{< figure src="./02-transformation/custom-function9.png" width=70% >}}

**Bước 2:** Tạo một parameter tham chiếu đến file mẫu trên.

{{< figure src="./02-transformation/custom-function10.png" width=50% >}}

**Bước 3:** Tạo một query đặt tên là _Transform Sample File_ sử dụng tham số trên

```
= #"Sample File Parameter"
```

**Bước 4:** Click chuột phải vào _Transform Sample File_, chọn _Create function_ và đặt tên cho function của chúng ta là _Transform File Function_

**Bước 5:** Quay trở lại thực hiện các thao tác biến đổi trên _Transform Sample File_ để có được một bảng dữ liệu ưng ý, function đã tạo sẽ tự động thêm các bước mà chúng ta chỉnh sửa vào.

Kết quả:

{{< figure src="./02-transformation/custom-function11.png" width=70% >}}

Về cách áp dụng hàm mới tạo thì tương tự như phần trên.

## 3. Combine or Append

Dữ liệu, không phải lúc nào cũng ở trong một files duy nhất. Đôi lúc, chúng ta cần phải tìm cách tập hợp dữ liệu trong nhiều files vào một file. Tùy vào cấu trúc của các files dữ liệu mà chúng ta có hai cách để làm điều này:

- Combine hoặc Append với các files có cấu trúc giống nhau.
- Merge với các files có một mối quan hệ nhất định ví dụ giống như CSDL quan hệ.

Trong phần này, ta sẽ đi tìm hiểu về **Combine** và **Append** query, còn về _Merge_ ta sẽ tìm hiểu ở phần tiếp theo.

Giả sử ta có bốn bảng dữ liệu như sau, các bảng có cấu trúc giống nhau (tên cột giống nhau, kiểu dữ liệu của các cột giống nhau):

{{< figure src="./03-combind-query/append-query.png" >}}

Để kết hợp dữ liệu của các bảng với nhau, ta vào _Home -> Append Queries -> Append Queries as New_

{{< figure src="./03-combind-query/Append-Queries-as-New.png" >}}

Bạn có thể chọn hai bảng để Append:

{{< figure src="./03-combind-query/basic-append.png" width=70% >}}

Hoặc chọn nhiều bảng để Append:

{{< figure src="./03-combind-query/more-append.png" width=70% >}}

Sau khi chọn xong, các bạn click vào OK để hoàn tất.

**Lưu ý**: Power Query kết hợp các bảng dữ liệu với nhau dựa vào tên cột. Nếu tên cột khác nhau thì với mỗi tên cột nó sẽ tạo ra một cột mới.

## 4. Merge

{{< figure src="./04-merge/Home-Merge-Queries.png" >}}

Chúng ta có thể nghĩ về cách hoạt động của Merge tương tự như sử dụng VLOOKUP trong Excel để tìm kiếm giá trị, hoặc phép JOIN trong SQL để merge nhiều bảng với nhau.

Giả sử ta có ba bảng dữ liệu như sau và đã được load vào Power Query:

{{< figure src="./04-merge/Power-Query-Merge-Source-Data.png" >}}

Để Merge bảng Sales với bảng Customers, ta vào _Home -> Merge Queries -> Merge Queries as New_

{{< figure src="./04-merge/Merge-Window-Options.png" width=80% >}}

Chúng ta thực hiện theo 3 bước sau:

- Bước 1: Chọn bảng dữ liệu ở **_(1)_** và **_(2)_**.
- Bước 2: Chọn cột dữ liệu thể hiện sự liên kết giữa hai bảng ở _**(3)**_.
- Bước 3: Chọn kiểu merge.

Trong Power Query hỗ trợ 6 kiểu merge dữ liệu cơ bản:

{{< figure src="./04-merge/join-type.webp" width=80% >}}

Trong ví dụ này, mình chọn _Left Outer_:

{{< figure src="./04-merge/left-outer.png" width=80% >}}

Cuối cùng, ta click vào icon ở cột Customers để chọn các cột từ bảng Customers muốn thêm vào bảng Sales.

## 5. Data quality

Trong thế giới của những người làm việc với dữ liệu có một câu nói thế này: _"Garbage in, garbage out. (GIGO)"_, hiểu nôm na thì các insights bạn tìm kiếm được từ dữ liệu chỉ thực sự tốt khi dữ liệu đầu vào được đảm bảo chất lượng. Vậy một bộ dữ liệu như thế nào mới là dữ liệu tốt?

Không có định nghĩa cụ thể về dữ liệu tốt, nhưng có một số tiêu chí được sử dụng để đánh giá chất lượng của bộ dữ liệu. Một bộ dữ liệu được gọi là tốt nếu thỏa mãn các tiêu chí sau:

{{< figure src="./05-data-quality/data_quality.webp" width=80% >}}

**Validity** _(Tính hợp lệ)_: Một tập dữ liệu cần tuân phải theo một số quy tắc, ràng buộc đã đặt ra. Ví dụ:

- Các giá trị trong một cột phải có kiểu dữ liệu cụ thể.
- Các giá trị số, hoặc ngày tháng thường nên nằm trong một phạm vi nhất định.
- Một số cột không được có giá trị _missing value_.
- Một số cột chỉ chứa các giá trị khác nhau, không được lặp lại (ví dụ các cột khóa).
- Cột khóa ngoại không thể chứa các giá trị không nằm trong khóa chính được tham chiếu.
- Một số cột giá trị nằm trong một tập hợp nào đó (ví dụ giới tính nam hoặc nữ).
- Một số cột phải tuân theo một định dạng nhất định (ví dụ số điện thoại).
- Một số cột phải tuân theo một điều kiện nào đó.

**Accuracy** _(Độ chính xác)_: Các giá trị thu thập được có chính xác và phản ánh chặt chẽ thực tế không?

**Completeness** _(Tính đầy đủ)_: Dữ liệu phải thu thập theo yêu cầu đã đầy đủ chưa? Giá trị thu thập được bị thiếu hoặc thiếu một phần được gọi là không đầy đủ.

**Consistency** _(Tính nhất quán)_: Giá trị liên quan đến một đối tượng ở trên toàn hệ thống phải giống nhau. Ví dụ địa chỉ của một người không thể ở bảng dữ liệu này là một địa chỉ, ở trong báo cáo nọ lại là một địa chỉ khác.

**Relevancy** _(Mức độ liên quan)_: Dữ liệu được thu thập có liên quan đến mục tiêu của tổ chức, mục tiêu phân tích hay không.

**Timeliness** _(Tính kịp thời)_: Dữ liệu về một sự kiện, hiện tượng hoặc đối tượng nghiên cứu nào đó phải được thu thập càng sớm càng tốt khi nó vừa xuất hiện.

**Uniformity** _(Tính đồng nhất)_: Sự đồng nhất về đơn vị đo lường trên toàn bộ hệ thống.

## 6. Data cleaning

Đôi khi, dữ liệu được sử dụng để phân tích có thể không mang lại kết quả mong muốn. Một trong những nguyên nhân gây ra là do dữ liệu của bạn chưa được tốt. Trong phần này, mình giới thiệu một cách tiếp cận gồm ba bước để có một tập dữ liệu tốt.

- Bước 1: Tìm hiểu rõ ràng về tập dữ liệu.
- Bước 2: Xác định trạng thái mong muốn về tập dữ liệu (tập dữ liệu tốt).
- Bước 3: Xác định các bước cần thiết để biến đổi tập dữ liệu hiện có thành tập dữ liệu mong muốn.

Để minh họa, giả sử ta có một tập dữ liệu như sau (Ví dụ và hình ảnh trong phần này được lấy từ sách _Tableau Prep: Up & Running_ của _Carl Allchin_):

{{< figure src="./06-data-cleaning/data-cleaning.png" >}}

### 6.1. Tìm hiểu về tập dữ liệu

{{< figure src="./06-data-cleaning/understanding-dataset.png" width=79% >}}

| Phân tích                                          | Ví dụ                                                                                                                                              |
| -------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cấu trúc của tập dữ liệu: hàng, cột hay crosstabs? | Có hai cột có kiểu categorical là BRANCH và PRODUCT. Với các cột còn lại thì mỗi một cột đại diện cho giá trị trong một tháng, có kiểu dữ liệu số. |
| Các cột và tiêu đề có đúng chuẩn chưa?             | Tiêu đề tháng nên nằm trong một cột, và các giá trị nằm trong một cột khác.                                                                        |
| Các kiểu dữ liệu của mỗi cột là gì?                | Mỗi cột chỉ nên có một kiểu dữ liệu.                                                                                                               |
| Mỗi hàng thể hiện điều gì?                         | Mỗi hàng, là số lượng các PRODUCT của các BRANCH khác nhau được bán trong một thời gian cụ thể.                                                    |
| Có giá trị bị thiếu trong tập dữ liệu không?       | Tập dữ liệu hiện tại không có _missing value_                                                                                                      |
| Số lượng quan sát có đúng như kỳ vọng?             | Trong ví dụ này chúng ta có 6 quan sát.                                                                                                            |
| Các quy tắc khác?                                  | Lewisham nên là một giá trị duy nhất thay vì tách thành hai.                                                                                       |

### 6.2. Tidy data

Trước khi đi xác định trạng thái mong muốn, ta cần phải hiểu một tập dữ liệu như thế nào được gọi là đúng chuẩn. Thì mình sẽ sử dụng khái niệm _"Tidy data"_ của _Hadley Wickham_. Hiểu nôm na thì thế này:

- Mỗi một biến mà bạn đo lường nên nằm trong một cột khác nhau.
- Mỗi một quan sát về một đối tượng nên nằm trong cùng một dòng.
- Mỗi một giá trị nằm trong một ô riêng biệt.

Về cơ bản ta có thể hiểu đơn giản là trong một bảng thì với mỗi một cột, một hàng hoặc một quan sát chỉ mang một ý nghĩa duy nhất. Đồng thời không thể có nhiều hàng, cột hoặc quan sát cùng thể hiện một ý nghĩa.

Minh họa:

{{< figure src="./06-data-cleaning/tidy-1.png" width=80% >}}

Tập dữ liệu bên dưới không thỏa mãn điều kiện thứ nhất, khi `cases` và `population` nằm trong một cột. Nó nên được tách thành hai cột riêng biệt.

{{< figure src="./06-data-cleaning/tidy-5.png" width=80% >}}

Tập dữ liệu tiếp theo không thỏa mãn điều kiện thứ ba, vì nó đã gộp giá trị của `cases` và `population` vào cùng một ô.

{{< figure src="./06-data-cleaning/tidy-6.png" width=80% >}}

Cuối cùng là một ví dụ không thỏa mãn điều kiện thứ nhất và thứ hai: Biến thời gian không nằm trong một cột, và quan sát về một đối tượng bị tách thành hai bảng.

{{< figure src="./06-data-cleaning/tidy-7.png" width=80% >}}

Một số ví dụ khác về cách trình bày dữ liệu không tốt _(click vào ảnh để xem rõ hơn)_:

{{< image src="./06-data-cleaning/tidy-8.png" caption="[Nguồn: Miles McBain](https://medium.com/@miles.mcbain/tidying-the-australian-same-sex-marriage-postal-survey-data-with-r-5d35cea07962)" >}}

{{< image src="./06-data-cleaning/tidy-9.png" caption="[Nguồn: Sharla Gelfand](https://sharlagelfand.netlify.app/posts/tidying-toronto-open-data/)" >}}

### 6.3. Xác định trạng thái mong muốn

Quay trở lại với ví dụ ban đầu, sau khi đã hiểu các khái niệm về _"Tidy data"_, chúng ta có thể phác thảo ra một tập dữ liệu mong muốn như sau:

{{< figure src="./06-data-cleaning/dataset-expect.png" width=80% >}}

{{< figure src="./06-data-cleaning/dataset-expect2.png" width=80% >}}

### 6.4. Các bước làm sạch

{{< figure src="./06-data-cleaning/data-cleaning-process.png" width=80% >}}

Đầu tiên, hãy nhìn vào các cột dữ liệu:

- Xác định các cột dữ liệu cần thiết và xóa các cột không cần thiết, hoặc sử dụng UNPIVOT để chuyển cột thành hàng nếu chúng đại diện cho cùng một thứ (ví dụ ngày tháng...).
- Có cột dữ liệu nào bị thiếu không, nếu thiếu có thể tạo cột mới hoặc JOIN/MERGE từ các bảng khác.
- Tên của các cột có thể hiện ý nghĩa cụ thể không?
- Kiểu dữ liệu trong các cột?

Tiếp theo, ta nhìn vào các quan sát:

- Số lượng các quan sát có như kỳ vọng không, lọc ra các quan sát không cần thiết.
- Các giá trị trong các ô có chính xác không (các lỗi về chính tả, _dirty data_).
- Có giá trị _missing value_ và _outliers_ không.

## 7. Dirty data

## 8. Missing values

## 9. Outliers

**Tóm lại**, khi chuẩn bị dữ liệu chúng ta sẽ gặp bốn vấn đề cơ bản sau:

{{< figure src="./06-data-cleaning/data-issue.png" width=50% >}}

Check list công việc để có được một tập dữ liệu tốt:

| Issues          | Check List                                               |
| --------------- | -------------------------------------------------------- |
| Data source     | Enough data _(Dữ liệu có đủ hay không)_                  |
|                 | Up to date _(Dữ liệu đã được cập nhật chưa)_             |
| Data types      | Data types correctly _(Kiểu dữ liệu có chính xác không)_ |
| Dirty data      | Not parsed correctly                                     |
|                 | Extra characers                                          |
|                 | Unexpected pattern                                       |
|                 | Incorrect data                                           |
|                 | Duplicate data records                                   |
|                 | Misspelled entries                                       |
| Missing data    | Deleting missing data                                    |
|                 | Imputation                                               |
|                 | Advanced methods                                         |
| Outliers        | Errors: cross-check & fix                                |
|                 | Errors: delect                                           |
|                 | No certainty: remove if insignificant                    |
|                 | Certainty: truncation                                    |
| Data formatting | Transposing _(Xoay bảng, Pivot, Unpivot)_                |
|                 | Aggregating data                                         |
|                 | Cross tabulation                                         |
| Data blending   | Unions                                                   |
|                 | Joins                                                    |
|                 | Fuzzy matching                                           |
|                 | Spatial matching                                         |

## 10. Consolidate
