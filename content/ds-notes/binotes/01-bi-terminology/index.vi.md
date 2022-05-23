---
title: "Day 1 - Một số thuật ngữ trong BI"
subtitle: ""
slug: 01-bi-terminology
date: 2022-05-20
lastmod: 2022-05-20
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["BI"]
categories: []
series: [BI Course Notes]
series_weight: 1
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

## 1. Data là gì?

Dữ liệu **_(data)_** là gì? Thực sự mình cũng không biết phải định nghĩa như nào, vì có quá nhiều định nghĩa về dữ liệu. Nhưng nếu hiểu theo cách nôm na thì dữ liệu là mọi thứ xung quanh chúng ta, ví dụ như tên, tuổi, giá sản phẩm,...

Mình nhớ hình như trong môn tin học lớp 10 cũng có một định nghĩa về data như thế này:

Chúng ta sẽ bắt đầu với khái niệm về _thông tin_. Thông tin là sự hiểu biết của con người về một thực thể nào đó, được thể hiện dưới dạng các tín hiệu như chữ số, âm thanh, hình ảnh,...mà chúng ta có thể thu thập, lưu trữ và xử lý được. Thì dữ liệu là các thông tin đã được mã hóa trên máy tính.

## 2. Cấu trúc dữ liệu

### 2.1. Structured data

Dữ liệu có cấu trúc thường là dữ liệu được lưu trữ ở dưới dạng bảng, ví dụ như các bảng dữ liệu trong Excel và database,...Mỗi một bảng dữ liệu gồm các dòng và các cột. Các cột thường đại diện cho các biến hoặc thuộc tính còn các dòng thì đại diện cho các quan sát, record...Ví dụ:

{{< figure src="./structured-data-1.png" width=65% >}}

### 2.2. Semi-structured data

Dữ liệu bán cấu trúc (mình không biết dịch như vậy có chuẩn không nữa), đây là những dữ liệu không được lưu trữ ở dưới dạng bảng như dữ liệu có cấu trúc nhưng lại có một cấu trúc nhất định. Ví dụ như dữ liệu lưu trữ trong các file `xml, json`:

{{< figure src="./structured-data-2.png" width=65% >}}

### 2.3. Unstructured data

Dữ liệu phi cấu trúc là những dữ liệu được lưu trữ ở định dạng mà chúng ta không thể xác định được cấu trúc của chúng. Ví dụ như dữ liệu lưu trữ trong các file `pdf`, hình ảnh, video, âm thanh, email...

## 3. Kiểu dữ liệu

Kiểu dữ liệu là một khái niệm khá quan trọng khi chúng ta sử dụng các ngôn ngữ lập trình như Python, R... hoặc là các công cụ xử lý dữ liệu như SQL, Excel, Power BI,...

Vậy kiểu dữ liệu là gì? Ta có thể hiểu nôm na đó là cách chúng ta lưu trữ thông tin ở trên máy tính. Mỗi một thuộc tính, đều có một kiểu dữ liệu xác định. Với mỗi một công cụ, đều có những cách phân loại khác nhau nhưng tóm lại nó có thể được quy về một trong 5 loại sau:

- _Strings_: là tập hợp các ký tự alphanumeric `a-zA-Z, 0-9` và một số ký tự đặc biệt.
- _Numeric_: là các số bao gồm số nguyên và số thập phân.
- _Date/Time_: là các dữ liệu miêu tả ngày tháng, thời gian hoặc kết hợp cả ngày tháng và thời gian.
- _Boolean_: là kiểu dữ liệu chỉ có hai giá trị đại diện cho `True` và `False`.
- _Special Objects_: là các kiểu dữ liệu đặc biệt như hình ảnh, âm thanh, video, maps,...

{{< admonition type=notes title="Data Formats" open=true >}}

Lưu ý là mặc dù kiểu dữ liệu được phân thành 5 loại, nhưng với mỗi loại lại có nhiều định dạng _(formats)_ khác nhau tùy thuộc vào từng công cụ. Ví dụ như kiểu Date/Time trong Excel:

{{< figure src="./data-formats.png" width=60% >}}
{{< /admonition >}}

## 4. Pivot và stacked

Sau này, khi xử lý dữ liệu, một trong những thao tác biến đổi chúng ta có thể sẽ phải làm là chuyển đổi định dạng _(số chiều, kích thước)_ của bảng dữ liệu.

### 4.1. Pivot

Pivot hiểu đơn giản thì nó được sử dụng để tạo ra một bảng mới tổng hợp dữ liệu từ một bảng dữ liệu nào đó. Dễ hình dung là tính năng PivotTable trong Excel.

{{< image src="./pivoting_simple1.png" width=75% caption="Pivoting Simple" >}}

{{< image src="./pivoting_simple_multicolumn.png" width=75% caption="Multi-column Pivoting" >}}

{{< image src="./pivoting_table_simple1.png" width=75% caption="Pivot Table" >}}

### 4.2. Stacked và unstacked

- Stacked (đôi khi gọi là _narrow format_)
- Unstacked (đôi khi gọi là _wide format_)

{{< figure src="./stakc_unstack-1.png" width=75% >}}

{{< figure src="./stack-simple2.png" width=75% >}}

## 5. Analysis và analytics

### 5.1. Data analysis

**_Data Anaysis_** là quá trình đi tìm câu trả lời cho những câu hỏi như _What, How, Why_ từ dữ liệu trong **quá khứ** hay nói một cách khác là cách chúng ta đặt câu hỏi và thu thập những hiểu biết từ những thông tin đã có. Ví dụ như: Doanh thu tháng trước của sản phẩm X là bao nhiêu, tại sao doanh số của sản phẩm đó vào mùa hè lại giảm mạnh,...

### 5.2. Data analytics

_**Data Analytics**_ là một quá trình sử dụng các công cụ bao gồm thu thập, xử lý, phân tích thống kê, mô hình hóa và khám phá dữ liệu trong **quá khứ** để tìm ra các insights có giá trị hỗ trợ cho các **quyết định** trong tương lai.

## 6. Kiểu dữ liệu trong thống kê

### 6.1. Cross-sectional data

Dữ liệu chéo _(Cross-sectional data)_ là các dữ liệu thu thập được từ **nhiều đối tượng** trong **một khoảng thời gian** nhất định. Ví dụ:

- Điểm của các sinh viên vào cuối học kỳ hiện tại.
- Tiền lương của người lao động năm 2020 - bao gồm các biến như tiền lương, trình độ học vấn, giới tính, kinh nghiệm,...

### 6.2. Time series data

{{< figure src="./time-series.jpg" width=80% >}}

Dữ liệu chuỗi thời gian _(Time series data)_ là các quan sát về một hoặc nhiều biến theo thời gian. Ví dụ:

- Giá cổ phiếu, tỷ giá hối đoái.
- Chỉ số giá tiêu dùng (CPI), tổng sản phẩm trong nước (GDP).
- Doanh thu theo ngày, tháng, quý, năm của một công ty.

### 6.3. Panel data

Dữ liệu mảng _(Panel data)_ là kiểu dữ liệu kết hợp hai loại trên. Ví dụ vẫn là bảng dữ liệu về tiền lương của người lao động trong phần trên nhưng được thu thập trong nhiều năm, chứ không phải chỉ riêng năm 2020. Một ví dụ khác:

{{< figure src="./panel-data-1.png" width=50% >}}

Các bạn có thể tưởng tượng dữ liệu chéo và dữ liệu chuỗi thời gian là dữ liệu ở dạng 2 chiều, còn dữ liệu mảng thì ở dạng 3 chiều.

{{< figure src="./panel-data-2.png" width=65% >}}

## 7. Thang đo trong thống kê

{{< figure src="./scales-of-measurement.png" >}}

Trong quá trình thu thập dữ liệu, với mỗi biến chúng ta phải quyết định xem nên sử dụng thang đo gì với biến đó. Thang đo sẽ quyết định lượng thông tin được chứa trong các biến và cách chúng ta tóm tắt và lựa chọn các chart, phương pháp phân tích thống kê phù hợp nhất.

Cấp độ phân chia đầu tiên, dữ liệu được chia làm hai nhóm:

- Dữ liệu định tính _(Categorical, quanlitative)_
- Dữ liệu định lượng _(Numerical, quantitative)_

### 7.1. Dữ liệu định tính

Dữ liệu định tính là dữ liệu liên quan đến mô tả, chúng ta có thể quan sát nhưng không thể đo lường được bằng các con số. Dữ liệu định tính thường là các nhãn, tên dùng để phản ánh tính chất, sự hơn kém hoặc phân loại các phần tử. Ví dụ như giới tính, màu sắc,...

### 7.2. Dữ liệu định lượng

Dữ liệu định lượng là dữ liệu mà chúng ta có thể sử dụng các con số để miêu tả mức độ của các quan sát. Ví dụ như khoảng cách, chiều dài, tốc độ, trọng lượng...

Dữ liệu định lượng lại được chia làm hai loại: Rời rạc và liên tục.

Dữ liệu rời rạc _(discrete)_: hiểu đơn giản là những dữ liệu được miêu tả bằng các số nguyên, giá trị rời rạc, hữu hạn. Ví dụ số lượng con mèo của một shop bán pet, ta có thể có 2 con mèo, ba con mèo, nhưng không thể nào có 2.5 con mèo được. Số nhà bán được trong một tháng cũng tương tự, chúng ta có thể bán được một cái nhà, hai cái nhà nhưng làm sao có thể bán nửa cái nhà.

Dữ liệu liên tục _(continuous)_: là dữ liệu mà các giá trị miêu tả có thể chia nhỏ thành các phần thập phân. Ví dụ như chiều cao hoặc cân nặng. Thời gian cũng có thể chia nhỏ thành nửa giây, nửa phút, nửa giờ.

### 7.3. Bốn loại thang đo

Dữ liệu định tính sử dụng hai loại thang đo:

- Thang đo định danh _(Nominal)_
- Thang đo thứ bậc _(Ordinal)_

Dữ liệu định lượng sử dụng hai loại thang đo:

- Thang đo khoảng _(Interval)_
- Thang đo tỷ lệ _(Ratio)_

{{< figure src="./measurements.jpg" width=80% >}}

Khi dữ liệu của một biến bao gồm các nhãn hoặc tên được sử dụng để phân biệt một thuộc tính của phần tử, thang đo này được gọi là **thang đo định danh**. Ví dụ, thị trường chứng khoán _(New York = 1, Nasdaq = 2)_, thì 1 và 2 là các nhãn trong đó 1 đại diện cho thị trường chứng khoán New York, còn 2 thì biểu thị cho thị trường chứng khoán Nasdaq. Trong trường hợp này, 1 và 2 là các nhãn phân biệt nơi cổ phiếu được giao dịch.

Thang đo, đối với một biến được gọi là **thang đo thứ bậc** nếu dữ liệu thể hiện tính chất của dữ liệu danh nghĩa và thứ tự hoặc xếp hạng của dữ liệu này có ý nghĩa. Ví dụ sự hài lòng của khách hàng _(xuất sắc, tốt, kém)_.

Thang đo, đối với một biến là **thang đo khoảng** nếu dữ liệu có tất cả các thuộc tính của **thang đo thứ bậc** và khoảng cách giữa các giá trị được thể hiện dưới dạng đơn vị đo lường cố định có ý nghĩa. Ví dụ ba học sinh với điểm _(SAT)_ là 620, 550 và 470 có thể được xếp hạng theo thứ tự từ thành tích tốt nhất đến kém nhất. Ngoài ra chênh lệch giữa các điểm số cũng có ý nghĩa.

Thang đo, đối với một biến là **thang đo tỷ lệ** nếu dữ liệu có tất cả các đặc tính của **thang đo khoảng** và tỷ lệ của hai giá trị có ý nghĩa. Ví dụ các biến như khoảng cách, chiều cao, trọng lượng, thời gian,...Thang đo này đòi hỏi một giá trị `0` đúng nghĩa, nghĩa là tại giá trị `0` không có gì tồn tại trong biến. Ví dụ chi phí của một ô tô, một giá trị `0` cho chi phí cho biết ô tô này là miễn phí.
