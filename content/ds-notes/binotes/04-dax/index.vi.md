---
title: "Day 4 - Data Analysis eXpressions"
subtitle: ""
slug: 04-dax
date: 2022-05-28
lastmod: 2022-05-28
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["BI"]
categories: []
series: [BI Course Notes]
series_weight: 4
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

{{< figure src="./dax.png" >}}

Cho đến nay, chúng ta đã biết, đằng sau nhiều thao tác xử lý và phân tích dữ liệu bên trong Power BI là sự xuất hiện của hai ngôn ngữ: **M Code** và **DAX**. Power BI sử dụng M để xây các thao tác xử lý, biến đổi và làm sạch dữ liệu trong Power Query trước khi chuyển dữ liệu vào trong Data models. Vậy còn DAX là gì?

DAX là một tập hợp các hàm, toán tử và hằng số có thể được sử dụng trong một công thức hoặc biểu thức, để tính toán và trả về một hoặc nhiều giá trị.

## 1. Basic Concepts

### 1.1. DAX syntax

{{< figure src="./dax-syntax.png" >}}

Nếu như các bạn từng sử dụng Excel, thì trong Excel hầu hết các công thức tính toán được tính toán dựa trên các ô _(Cell)_ trong bảng tính. Tuy nhiên với DAX chúng ta sẽ cần thay đổi tư duy một chút, các công thức DAX được tính toán dựa trên các cột dữ liệu hoặc bảng dữ liệu.

Một số lưu ý khi tham chiếu dữ liệu trong DAX:

- Nếu mà tên của bảng dữ liệu chứa khoảng trắng thì ta phải đặt nó bên trong dấu ngoặc: `'Table Name'`
- Để tham chiếu đến một cột trong bảng dữ liệu chúng ta sử dụng cú pháp: `Table[Column]`
- Để tham chiếu đến các chỉ số (measures), chúng ta sử dụng cú pháp: `[measures_name]`
- DAX không phân biệt giữa các ký tự in hoa và in thường.

### 1.2. Toán tử

**Toán tử cơ bản:**

| Toán tử | Ý nghĩa   |  Ví dụ   |
| :-----: | --------- | :------: |
|    +    | Phép cộng | `3 + 3`  |
|    -    | Phép trừ  | `3 - 2`  |
|   \*    | Phép nhân | `3 * 3`  |
|    /    | Phép chia | `3 / 2`  |
|    ^    | Lũy thừa  | `16 ^ 4` |

**Toán tử so sánh**

| Toán tử | Ý nghĩa                  | Ví dụ                         |
| :-----: | ------------------------ | ----------------------------- |
|    =    | So sánh bằng             | `[Region] = "USA"`            |
|   ==    | So sánh bằng (chính xác) | `[Region] == "USA"`           |
|   <>    | So sánh không bằng       | `[Region] <> "USA"`           |
|    >    | Lớn hơn                  | `[Sales Date] > "Jan 2009"`   |
|   >=    | Lớn hơn hoặc bằng        | `[Amount] >= 20000`           |
|    <    | Nhỏ hơn                  | `[Sales Date] < "Jan 1 2009"` |
|   <=    | Nhỏ hơn hoặc bằng        | `[Amount] <= 100`             |

**Lưu ý:** tất cả các phép so sánh ngoại trừ toán tử `==` thì BLANK có thể được hiểu là _DATE(1899, 12, 30), 0, FALSE, "" (empty string)_ tùy thuộc vào kiểu dữ liệu của cột so sánh. Ngược lại thì `[Column] == 0` sẽ trả về TRUE khi và chỉ khi giá trị trong cột `[Column]` là 0.

**Toán tử logic**

| Toán tử | Ý nghĩa                             | Ví dụ                                                |
| :-----: | ----------------------------------- | ---------------------------------------------------- |
|  `&&`   | Toán tử AND                         | `([Region] = "France") && ([BikeBuyer] = "yes"))`    |
| `\|\|`  | Toán tử OR                          | `(([Region] = "France") \|\| ([BikeBuyer] = "yes"))` |
|   IN    | Kiểm tra sự tồn tại của các giá trị | `'Product'[Color] IN { "Red", "Blue", "Black" }`     |

**Toán tử nối chuỗi**

| Toán tử | Ý nghĩa                                  | Ví dụ                      |
| :-----: | ---------------------------------------- | -------------------------- |
|   `&`   | Nối một hoặc nhiều chuỗi thành một chuỗi | `[Region] & ", " & [City]` |

### 1.3. Một số hàm phổ biến

{{< figure src="./learning-dax.png" width=75% >}}

**Hàm tổng hợp dữ liệu**

```
SUM(ColumnName)             // Tính tổng

AVERAGE(ColumnName)         // Tính trung bình

MAX(ColumnName)             // Tìm giá trị lớn nhất

MAX(Scalar1, Scalar2,...)   // Tìm giá trị lớn nhất

MIN(ColumnName)             // Tìm giá trị nhỏ nhất

MIN(Scalar1, Scalar2,...)   // Tìm giá trị nhỏ nhất

// Phép chia tử số cho mẫu số và giá trị thay thế nếu gặp lỗi
DIVIDE(Numerator, Denominator, AlternateResult)
```

```
COUNT(ColumnName)           // Đếm số hàng chứa giá trị số trong một cột

COUNTA(ColumnName)          // Đếm số hàng không rỗng trong một cột

DISTINCTCOUNT(ColumnName)   // Đếm số lượng các giá trị duy nhất trong một cột

COUNTROWS(Table)            // Đếm số hàng trong một bảng
```

**Hàm về ngày tháng, thời gian**

```
DAY/MONTH/YEAR(Date)                   // Trích thông tin từ Date

HOUR/MINUTE/SECOND(DateTime)           // Trích thông tin từ Date

TODAY()                                // Trả về ngày hiện tại

NOW()                                  // Trả về thời điểm hiện tại

WEEKDAY/WEEKNUM(Date, [Return Type])   // Thứ trong tuần

EOMONTH(StartDate, Months)             // EOM = End of Month

DATEDIFF(Date1, Date2, Interval)       // Khoảng chênh lệch giữa 2 Date
```

**Hàm Logic**

```
IF(Dieu_kien, Result_if_True, Result_if_False)

IFERROR(Value, Value_if_Error)

AND(Dieu_kien_A, Dieu_kien_B)          // True nếu cả 2 đều trả về True

OR(Dieu_kien_A, Dieu_kien_B)           // True nếu một trong hai trả về True

SWITCH (expression, value1, result1, value2, result2,…, other_value)
```

**Hàm xử lý Text**

```
LEN(Text)                              // Số lượng ký tự của một chuỗi

CONCATENATE(Text1, Text2)              // Nối hai chuỗi thành một chuỗi

LEFT/RIGHT(Text, number)               // Trả về tập hợp các ký tự từ trái hoặc phải

MID(Text, StartPosition, Number)       // Trả về tập hợp các ký tự từ StartPosition

UPPER/LOWER/PROPER(Text)               // Chuyển đổi giữa các ký tự in hoa và in thường

SUBSTITUTE(Text, old_text, new_text)   // Thay thế chuỗi các ký tự

SEARCH(FindText, WithinText)           // Tìm kiếm vị trí của FindText bên trong WithinText
```

### 1.4. Kiểu dữ liệu

Trong DAX, chúng ta sẽ thường gặp 6 kiểu dữ liệu sau:

- **Whole Number**: Số nguyên
- **Decimal Number**: Các số có phần thập phân
- **Currency**: Là Decimal Number nhưng có số lượng các chữ số phần thập phân là cố định
- **DateTime**: Kiểu dữ liệu ngày tháng, thời gian
- **Boolean**: Kiểu dữ liệu chỉ có hai giá trị `True` hoặc `False`
- **String**: Kiểu dữ liệu chuỗi

### 1.5. BLANK

Trong DAX, **BLANK** đại diện cho các giá trị NULLs, Missing values. Chúng ta thường gặp hai hàm sau:

- Hàm `BLANK()` được sử dụng để tạo giá trị BLANK.
- Hàm `ISBLANK()` được sử dụng để kiểm tra xem một giá trị có phải là BLANK hay không.

{{< figure src="./handling-blank.png" width=35% >}}

## 2. Calculated column

Sau khi chúng ta đã thiết kế xong Data models, đã kết nối các bảng dữ liệu với nhau thông qua các mối liên kết _(Relationships)_. Thì công việc tiếp theo chúng ta có thể làm là mở rộng, bổ sung thêm các thông tin cho Data models bằng cách:

- **Calculated columns:** Thêm các cột tính toán vào trong một bảng dữ liệu trong Data models. Việc thêm một cột vào trong Data models sẽ làm tăng kích thước của Data models đó và bộ nhớ khi chúng ta thực hiện các thao tác trong Power BI.
- **Measures:** được sử dụng để tính toán các **chỉ số** phân tích một vấn đề nào đó. Không như Calculated columns, các Measures không làm tăng kích thước của Data models, nó chỉ thực hiện các tính toán khi bị gọi đến ví dụ như ta vẽ các biểu đồ và reports.

### 2.1. Add Columns

Calculated columns được tính toán dựa trên các cột trong bảng dữ liệu. Và khi mình thực hiện tính toán thì các phép tính được thực hiện cho từng dòng của bảng dữ liệu.

{{< admonition type=notes title="Data Model" open=true >}}

Trước khi chúng ta đi thực hành, chúng ta cần có một Data Model. Bởi vì DAX được sử dụng để thêm các thông tin bổ sung cho Data Model, lưu ý là nó không tác động đến bảng dữ liệu trong Power Query.

Trong bài viết này, mình sử dụng một bộ [dữ liệu](./data/1%20DAX%20Sample%20Data.pbix) về bán hàng, sản phẩm ở đây là một số loại rượu vang (Wines).

{{< figure src="./data-model.png" width=85% >}}

Như các bạn có thể thấy thì Data model này gồm có 6 bảng:

- **Winesales**: Bảng Fact, các thông tin liên quan đến bán hàng.
- **Wines**: Thông tin về các sản phẩm được bán.
- **Customers**: Thông tin về khách hàng.
- **SalesPeople**: Thông tin về nhân viên bán hàng.
- **Regions**: Thông tin về khu vực mua hàng của khách hàng.
- **DateTable**: Thông tin về thời gian hằng ngày, được tính từ ngày bắt đầu bán hàng.
  {{< /admonition >}}

Để tạo Calculated columns, chúng ta vào Data View và chọn bảng dữ liệu cần thêm cột, sau đó trên thanh Ribbon ta vào menu _Table tools -> Calculations -> New Column_:

{{< figure src="./02-calculated-column/dax-start.jpg" width=70% >}}

Ví dụ với bảng **Winesales**:

{{< figure src="./02-calculated-column/add-column.png" >}}

Chúng ta có thể hình dung về các hoạt động tính toán trên Calculated columns nó gần giống với cách chúng ta tính toán trong Excel chỉ khác về cách tham chiếu.

{{< figure src="./02-calculated-column/row-context.jpg" >}}

Một số ví dụ khác:

```
Team =
IF (
    Winesales[SALESPERSON ID] = 1
    || Winesales[SALESPERSON ID] = 3
    || Winesales[SALESPERSON ID] = 6,
    "Team A",
    "Team B"
)
```

```
Volume =
IF (
    Winesales[CASES SOLD] >= 50
    && Winesales[CASES SOLD] <= 400,
    "High",
    "Low"
)
```

**Lưu ý**: Để xuống dòng trong khi viết các biểu thức DAX chúng ta sử dụng phím tắt _Shift + Enter_, để thực thi các câu lệnh chúng ta dùng _Enter_.

### 2.2. Hàm RELATED

Thông thường, khi tạo Calculated columns, chúng ta chỉ có thể sử dụng các cột trong cùng một bảng. Tuy nhiên, đôi lúc bạn sẽ cần lấy thông tin từ bảng khác. Khi đó chúng ta phải sử dụng hàm `RELATED(Table_Name[Columns])`, về cách hoạt động thì nó tương tự như hàm VLOOKUP trong Excel.

**Lưu ý**: Các bảng phải được liên kết với nhau và chúng ta chỉ có thể lấy được dữ liệu từ bảng _one side_ vào bảng _many side_ trong mối quan hệ One-to-Many.

{{< figure src="./02-calculated-column/related-column.png" width=80% >}}

Ví dụ: Chúng ta có thể lấy các dữ liệu từ hai bảng **Customers** và **Region** vào bảng **Winesales**:

```
Customer Name from Customers Table = RELATED( Customers[CUSTOMER NAME] )
```

```
REGION NAME = RELATED( Regions[REGION] )
```

{{< figure src="./02-calculated-column/related-column2.png" >}}

Chúng ta có thể sử dụng dữ liệu tham chiếu được từ trong các bảng khác trong công thức tính toán như sau:

```
SALES = Winesales[CASES SOLD] * RELATED( Wines[PRICE PER CASE] )
```

Tuy nhiên như đã nói ở trên thì Calculated columns được tính toán trên từng dòng của bảng dữ liệu. Bạn thử tưởng tượng, nếu bảng dữ liệu của chúng ta có số lượng dòng rất rất là lớn, khi đó sử dụng Calculated columns và RELATED sẽ làm tăng kích thước và ảnh hưởng đến hiệu suất hoạt động của Data models. Trong phần tiếp theo, chúng ta sẽ đi tìm hiểu một giải pháp giúp chúng ta giải quyết vấn đề này đó là Measures.

Chúng ta nên hạn chế tạo ra các Calculated columns và nếu có thể tạo nó trong Power Query thì chúng ta nên tạo nó trong Power Query. Thông thường, Calculated columns được sử dụng khi bạn muốn tạo ra các slicer, nhóm đối tượng, các điều kiện lọc hoặc là các giá trị trên một trục của đồ thị.

## 3. Measures

Measures được sử dụng để giúp chúng ta tạo ra các chỉ số phân tích ví dụ như KPIs,...Và nó chỉ thực hiện các tính toán khi chúng ta kéo thả các chỉ số vào báo cáo hoặc đồ thị. Không giống như Calculated columns, các Measures là một thành phần của Data models và nó không thuộc về bảng nào hết do đó chúng ta có thể để nó ở bất cứ đâu.

Measures được đánh giá dựa vào **filter context**, điều đó có nghĩa là khi chúng ta thay đổi các filter hoặc slicer trên báo cáo và đồ thị thì các chỉ số cũng được tính toán lại. Hoặc là khi chúng ta tạo ra các bảng tổng hợp dữ liệu (Summary Tables) theo các biến Category, thì các chỉ số sẽ được tính toán cho từng nhóm riêng biệt.

{{< figure src="./02-calculated-column/filter-context.png" >}}

### 3.1. Implicit Measures

Khi thực hiện kéo thả các trường trong Power BI vào reports, nếu để ý bạn sẽ thấy bên cạnh một số cột được tự động thêm vào ký hiệu sigma ( ∑ ). Ký hiệu này có hai ý nghĩa, một là chỉ ra rằng các cột này chứa dữ liệu là dữ liệu số, và hai là khi các trường này được kéo thả vào reports nó sẽ được tự động tổng hợp dựa vào một số chỉ số gọi là **Implicit Measures**.

{{< figure src="./03-measures/implicit-measures.jpg" >}}

Tuy nhiên, các chỉ số Implicit measures cũng có một số nhược điểm nhất định:

- Nếu bạn đổi tên `Average of CASE SOLD` thành một tên khác. Sau đó nếu bạn thay đổi _implicit measures_ thành một chỉ số khác thì bạn sẽ phải đổi lại tên này một lần nữa.
- Nếu bạn đổi tên _implicit measures_ thì tên của chỉ số trên đồ thị, reports sẽ không khớp với tên cột ở khu vực kéo thả Fields List.
- Trong một số trường hợp, bạn muốn format lại các giá trị tạo ra bởi _implicit measures_, nhưng mọi thao tác định dạng mà bạn thực hiện chỉ tồn tại ở thời điểm hiện tại. Khi bạn thay đổi tên cột, tên chỉ số hoặc sử dụng chỉ số này cho một cột khác thì bạn phải format lại từ đầu.

### 3.2. Explicit Measures

Các chỉ số Measures mà chúng ta tạo ra trên Data models của mình được gọi là **Explicit Measures**. Ngược lại với _implicit measures_ thì các chỉ số này có thể thực hiện hầu hết những vẫn đề mà _implicit measures_ gặp phải.

Các Measures thường được tạo trên bảng Fact hoặc người ta cũng có thể tạo một bảng Dummy chỉ để chứa các Measures trong đó. Để tạo một bảng lưu trữ các chỉ số, từ _Home Tab_ của thanh Ribbon, ta chọn _Enter Data_ và đặt tên bảng là **Measures Table**, sau đó thì load vào Data models. Dĩ nhiên là bạn hoàn toàn có thể đặt một cái tên khác cho bảng này.

Tiếp theo, chúng ta sẽ đi tạo một Measure trong bảng này. Để tạo một Measures thì tương tự như tạo Calculated Column, từ thanh Ribbon ta vào menu _Table tools -> Calculations -> New Measure_ hoặc click chuột phải vào bảng vừa tạo và chọn _New Measure_.

```
Total Cases = SUM( Winesales[CASES SOLD] )
```

**Lưu ý**: Trong Power Pivot của Excel khi viết các biểu thức DAX cho một Measures chúng ta phải sử dụng `:=` thay vì `=`.

{{< figure src="./03-measures/add-measures.png" >}}

Chúng ta thực hành tạo thêm một số chỉ số:

```
Avg Cases = AVERAGE( Winesales[CASES SOLD] )
```

```
No. of Sales = COUNTROWS( Winesales )
```

{{< figure src="./03-measures/more-measures.png" width=40% >}}

### 3.3. Filter Direction

Giả sử chúng ta có hai chỉ số như sau:

```
Total Cases = SUM( Winesales[CASES SOLD] )
```

```
Total Stores = SUM( Customers[NO. OF STORES] )
```

Và ta có một bảng tổng hợp dữ liệu sử dụng hai chỉ số trên:

{{< figure src="./03-measures/filter-direction2.png" width=40% >}}

Các bạn có thắc mắc là tại sao cột `Total Stores` lại chỉ trả về một giá trị duy nhất hay không. Chúng ta nhìn lại vào mối quan hệ giữa các bảng trong Data models:

{{< figure src="./03-measures/filter-direction.jpg" width=75% >}}

Hãy nhớ lại rằng:

- Bảng Dim là các bảng được sử dụng để phân loại, gom nhóm dữ liệu.
- Bảng Fact là bảng được sử dụng để tổng hợp dữ liệu sau khi gom nhóm.

Khi chúng ta phân loại dữ liệu theo bảng Dim **Wines**, thông tin sẽ được gửi đến bảng Fact **Winesales** để tổng hợp dữ liệu và chỉ có thể đến bảng này thôi. Chúng ta không thể đi từ bảng **Winesales** đến bảng **Customers** để lấy dữ liệu cho chỉ số `Total Store` vì chiều của _filter direction_ ở đây là một chiều _(single)_.

Vậy làm thế nào để giải quyết vấn đề này? Bạn hoàn toàn có thể thay đổi lại chiều của _filter direction_ nhưng các bạn không nên thay đổi trực tiếp trên Data Models mà DAX có một hàm có thể giúp chúng ta thay đổi nó. Mình sẽ trình bày về hàm này ở phần dưới. Tạm thời, chúng ta sẽ gác lại vấn đề này ở đây.

## 4. Iterators

{{< figure src="./04-iterators/sumx.png" width=75% >}}

Trong phần một, chúng ta đã đi nhanh qua một số hàm tổng hợp dữ liệu. Tuy nhiên các hàm này có một nhược điểm đó là chỉ áp dụng được cho các cột. Bây giờ giả sử bạn muốn tính SUM của một biểu thức thì không thể nào thực hiện được, do đó chúng ta cần một loại hàm thay thế gọi là các hàm **Iterators**. Đặc điểm của các hàm Iterators là sẽ có thêm `X` ở phía sau tên hàm.

Một số hàm thường sử dụng gồm có: _SUMX, AVERAGEX, MAXX, MINX, COUNTAX_. Về nguyên lý hoạt động, DAX sẽ tạo ra một cột ảo giống như Calculated columns dựa vào kết quả tính toán được của biểu thức bên trong hàm. Sau đó thì hàm iterators sẽ tổng hợp dữ liệu dựa trên cái cột dữ liệu ảo này.

{{< figure src="./04-iterators/sumx.jpg" width=75% >}}

Về mặt cú pháp thì một hàm iterators sẽ gồm hai thành phần: tên bảng và biểu thức tính toán.

{{< figure src="./04-iterators/iterator-syntax.png" width=80% >}}

Một số ví dụ:

```
Next Yr Cases Measure =
SUMX(
    Winesales,
    IF (Winesales[CASES SOLD] > 100,
        Winesales[CASES SOLD] * 1.2,
        Winesales[CASES SOLD] * 1.1
    )
)
```

```
Total Sales =
SUMX(
    Winesales,
    Winesales[CASES SOLD] * RELATED ( Wines[PRICE PER CASE] )
)
```

## 5. Variables

### 5.1. Khai báo biến

Mặc dù DAX không phải là một ngôn ngữ lập trình mà chỉ là một ngôn ngữ query nhưng chúng ta có thể khai báo biến bên trong DAX với cú pháp sau:

```
VAR <ten_bien> = <DAX expression>
RETURN <result_expression>
```

**Ví dụ minh họa:**

{{< figure src="./05-variable/variable.png" width=70% >}}

**Một số lưu ý về tên biến:**

- Không được sử dụng các tên mà trùng với các tên bên trong bảng, hoặc các từ khóa của DAX.
- Tên biến không được chứa khoảng trắng.
- Tên biến không được bắt đầu bằng các chữ số `0-9`
- Tên biến gồm các ký tự `a-z, A-Z, 0-9`

Các biến trong DAX, một khi được đánh giá tại một thời điểm thì chúng ta không thể thay đổi lại các giá trị của nó như các ngôn ngữ lập trình khác. Ví dụ sau đây sẽ gặp lỗi:

```
VAR my_var = 1
VAR my_var = 2
RETURN my_var
```

Một ví dụ khác: Filter trong hàm CALCULATE sẽ không ảnh hưởng đến `TotalOrders` bởi vì nó đã được đánh giá trước đó rồi.

{{< figure src="./05-variable/variable2.png" width=65% >}}

### 5.2. Formatting

Trong DAX không có công cụ hỗ trợ giúp ta sắp xếp lại đoạn Code của mình. Để định dạng lại chương trình, các bạn Copy đoạn Code của mình và vào trang web [DAX Formatter](https://www.daxformatter.com/) để tiến hành format, sau đó Copy trở lại ô công thức DAX trong Power BI.

Chúng ta có thể viết các comments để giải thích, ghi chú thêm về đoạn Code của mình bằng một số cách sau:

- `//` hoặc `--` đối với các ghi chú ngắn, được viết trên một dòng.
- `/* ... */` đối với các ghi chú dài, được viết trên nhiều dòng.

## 6. CALCULATE Function

Quan sát bảng dữ liệu sau và mối quan hệ giữa hai bảng **DateTable** và **Winesales**:

{{< figure src="./06-calculate/start.jpg" width=75% >}}

Giả sử có một yêu cầu phân tích tính tỷ lệ `%` của tổng số hàng bán được của mỗi loại rượu vang (Wine) trong năm 2021 so với số hàng bán được trong tất cả các năm như hình sau:

{{< figure src="./06-calculate/require.jpg" width=60% >}}

Như vậy chúng ta có thể chia yêu cầu trên thành ba bước tính:

- Tính số lượng hàng bán được của từng loại rượu: `Total Cases`
- Tính số lượng hàng bán được trong năm 2021 của từng loại rượu: `2021 Cases`
- Tính tỷ lệ: `2021 Case / Total Case`

Với mục tiêu đầu tiên khá là đơn giản, chúng ta đã tạo Measure này ở phần trên:

```
Total Cases = SUM( Winesales[CASES SOLD] )
```

Với mục tiêu thứ hai, chúng ta sẽ cần sử dụng hàm `CALCULATE` để điều chỉnh lại filter.

### 6.1. Cú pháp

{{< figure src="./06-calculate/calculate-syntax.jpg" width=80% >}}

- **Expression:** Một biểu thức DAX hoặc một chỉ số để tính toán tùy theo yêu cầu phân tích.
- **Filter**: Các điều kiện lọc dữ liệu, có thể có một hoặc nhiều điều kiện sau đó các điều kiện này được kết hợp với nhau.

Bây giờ ta sẽ quay trở lại với mục tiêu thứ hai ở trên:

```
2021 Cases = CALCULATE ( [Total Cases], DateTable[Year] = 2021)
```

Một lưu ý nữa ở đây, khi thực hiện bộ lọc `DateTable[Year] = 2021` trong bảng **DateTable** thì nó sẽ gửi yêu cầu này đến bảng **Winsales** để lấy dữ liệu tương úng (chú ý chiều của filter direction).

Tạm thời như vậy đã, chúng ta cần phải hoàn thành nốt mục tiêu thứ ba ở trên:

```
2021 Percentage = DIVIDE ( [2021 Cases], [Total Cases] )
```

**Lưu ý:** Không sử dụng hai cột trong cùng một filter, điều này nhiều khi sẽ gây ra những kết quả không chính xác.

### 6.2. Sử dụng nhiều filter

```
Total Cases in May 2021 =
CALCULATE (
    [Total Cases],
    DateTable[YEAR] = 2021,
    DateTable[MONTH] = "may"
)
```

```
Total Cases for Abel in Argentina =
CALCULATE (
    [Total Cases],
    SalesPeople[SALESPERSON] = "abel",
    Regions[REGION] = "argentina"
)
```

```
Average Cases for Black Ltd in 2021 =
CALCULATE (
    AVERAGE ( Winesales[CASES SOLD] ),
    DateTable[Year] = 2021,
    Customers[CUSTOMER NAME] = "black ltd"
)
```

### 6.3. Filter với OR

```
Total Cases 2020 or 2021 =
CALCULATE ( [Total Cases],
    DateTable[YEAR] = 2021
    || DateTable[YEAR] = 2020
)
```

```
Average Cases Argentina or Australia =
CALCULATE (
    AVERAGE ( Winesales[CASES SOLD] ),
    Regions[REGION] = "argentina"
    || Regions[REGION] = "australia"
)
```

```
Average Cases Argentina or Australia =
CALCULATE (
    AVERAGE ( Winesales[CASES SOLD] ),
    OR ( Regions[REGION] = "argentina",
        Regions[REGION] = "australia")
)
```

## 7. Table Functions

Table Functions là các hàm được sử dụng để tạo ra các bảng ảo (Virtual Table). Các bảng ảo này có thể là một tập hợp con của các hàng hoặc cột từ một bảng dữ liệu nào đó. Các hàm tạo bảng ảo luôn luôn phải được sử dụng làm tham số cho một hàm Scalar function.

### 7.1. Hàm FILTER

Hàm FILTER trả về một bảng là một tập hợp con của một bảng khác, cú pháp:

```
FILTER ( table , filter )
```

Trong đó:

- **table**: là tên bảng mà bạn muốn filter.
- **filter**: là điều kiện lọc bạn muốn áp dụng.

Ví dụ:

```
FILTER ( Wines, Wines[TYPE] = "red" )
```

Chúng ta thường sử dụng hàm FILTER như là một tham số lọc trong hàm CALCULATE. Trong phần trên, mình đã nói rằng không sử dụng hai cột trong cùng một filter. Tuy nhiên nếu là sử dụng hàm FILTER làm tham số lọc thì ngược lại, ta có thể sử dụng hai cột khi filter. Ví dụ:

```
Sales for Red or French=
CALCULATE (
    [Total Sales],
    FILTER ( Wines, Wines[TYPE] = "red"
                 || Wines[WINE COUNTRY] = "France" )
)
```

{{< figure src="./07-table-functions/filter.jpg" width=80% >}}

Một ví dụ nữa giải thích về cách thức hoạt động của hàm FILTER:

{{< image src="./07-table-functions/filter.png" width=100% >}}

### 7.2. Column Filters vs. Table Filters

Cho đến thời điểm hiện tại, chúng ta đã biết có hai cách để sửa đổi filter của một chỉ số:

- Sử dụng các filter dựa vào điều kiện của các cột.
- Sử dụng hàm FILTER làm điều kiện lọc, sẽ tạo ra một bảng ảo thay thế.

Thì hai phương pháp này có gì khác nhau?

Giả sử ta có hai chỉ số sau trả về một cùng kết quả nhưng sử dụng phương thức khác nhau:

```
Cases GT 300 #1 =
CALCULATE ([Total Sales], Winesales[CASES SOLD] > 300
```

```
Cases GT 300 #2 =
CALCULATE (
    [Total Sales],
    FILTER ( Winesales, Winesales[CASES SOLD] > 300 )
)
```

{{< figure src="./07-table-functions/table-vs-column-filter.jpg" width=60% >}}

Bây giờ chúng ta sẽ đi phân tích phương pháp filter đầu tiên, đó là filter dựa vào các cột:

{{< figure src="./07-table-functions/column-filter.jpg" width=80% >}}

Từ bảng tổng hợp dữ liệu theo **WINE**, mình giả sử đầu tiên sẽ đi tính toán các chỉ số cho `Grenache`, thì khi mà `Grenache` được filter trong **WINE**, nó được gửi đến **Winesales** để lọc ra các hàng chỉ chứa `Grenache`. Tiếp theo đó, nó lại áp dụng bộ lọc cho `CASES SOLD`. Và cuối cùng mới đi áp dụng chỉ số để tính giá trị tổng hợp cho trường hợp này.

{{< figure src="./07-table-functions/table-filter.jpg" width=80% >}}

Với phương pháp Table Filters, bước 1 và bước 2 tương tự như Column Filters, nhưng sau đó hàm FILTER sẽ lặp qua từng hàng trong bảng **Winesales** để lọc dữ liệu và tạo ra một bảng ảo mới. Cuối cùng sẽ áp dụng chỉ số để tính giá trị tổng hợp trên bảng ảo này.

Trong trường hợp dữ liệu của chúng ta quá lớn, việc tạo ra các bảng ảo không cần thiết sẽ làm tăng khối lượng và thời gian tính toán của chúng ta, làm chậm hoạt động của các Reports. Do đó chúng ta nên luôn luôn sử dụng Column Filters và chỉ sử dụng Table Filters nếu không thể sử dụng được Column Filters.

Đôi khi, Column Filters và Table Filters có thể sẽ trả về các kết quả không giống nhau. Ví dụ:

```
Bordeaux Wines #1 =
CALCULATE (
    SUM ( Winesales[CASES SOLD] ),
    Wines[WINE] = "Bordeaux" )
```

```
Bordeaux Wines #2 =
CALCULATE (
    SUM ( Winesales[CASES SOLD] ),
    FILTER ( Wines, Wines[WINE] = "Bordeaux" )
)
```

{{< figure src="./07-table-functions/table-vs-column-filter2.jpg" width=45% >}}

Chúng ta có thể hiểu đơn giản về trường hợp này như sau: Column Filters sẽ sửa đổi và ghi đè lên filter context nếu filter bị trùng lặp mỗi khi chỉ số được gọi. Còn hàm FILTER sẽ không sửa đổi filter context.

{{< figure src="./07-table-functions/column-filter2.jpg" caption="_Column Filters_" width=40% >}}

{{< figure src="./07-table-functions/table-filter2.jpg" caption="_Table Filters_" width=70% >}}

Trên thực tế, việc ghi đè filter khá là kỳ cục, tuy nhiên chúng ta có thể ngăn Column Filters ghi đè filter context bằng hàm KEEPFILTERS:

```
Bordeaux Wines #1 =
CALCULATE (
    SUM ( Winesales[CASES SOLD] ),
    KEEPFILTERS ( Wines[WINE] = "Bordeaux" )
)
```

## 8. Hàm ALL

Hàm ALL có hai chức năng, tùy thuộc vào vị trí mà nó đảm nhiệm:

- Khi hàm ALL là một Table Function, nó sẽ trả về tất cả các hàng của một bảng dữ liệu hoặc một cột dữ liệu gồm các giá trị riêng biệt sau khi đã remove duplicate.
- Khi hàm ALL là đối số Filter trong hàm CALCULATE thì nó sẽ xóa bỏ bộ lọc hiện tại từ các hàng và cột, hàm ALL không tạo ra bảng ảo.

Về mặt cú pháp, ALL chỉ nhận một đối số duy nhất là bảng dữ liệu cơ sở (không nhận bảng ảo), hoặc một tập hợp các cột. Ví dụ:

```
ALL ( Winesales )
ALL ( Wines[TYPE] )
```

### 8.1. ALL với Fact Table

Khi hàm ALL áp dụng với bảng Fact Table, nó sẽ tạo ra một bảng ảo bỏ qua tất cả các bộ lọc đến từ các bảng DIM.

{{< figure src="./08-all-func/all-with-fact.jpg" width=70% >}}

Ví dụ chúng ta có các chỉ số sau:

```
No. of Sales = COUNTROWS ( Winesales )
```

```
Grand Total No. of Sales = COUNTROWS ( ALL ( Winesales ) )
```

```
No. of Sales as Percent of Grand Total =
DIVIDE ( [No. of Sales] , [Grand Total No. of Sales] )
```

{{< figure src="./08-all-func/all-with-fact2.jpg" width=60% >}}

Trường hợp ALL bên trong CALCULATE: Nó không tạo bảng ảo, nó sẽ xóa bỏ tất cả các filter đã có trước đó.

```
Total Cases All Winesales =
CALCULATE ( [Total Cases], ALL( Winesales ) )
```

{{< figure src="./08-all-func/all-calculate.jpg" width=40% >}}

### 8.2. ALL với DIM Table

{{< figure src="./08-all-func/all-width-dim.jpg" width=60% >}}

Khi chúng ta sử dụng ALL với một bảng DIM nào đó, thì chỉ bộ lọc trên bảng đó bị bỏ qua, bộ lọc trên các bảng DIM khác vẫn sẽ ảnh hưởng đến bảng Fact.

Ví dụ:

```
No. of Sales = COUNTROWS ( Winesales)
```

```
No. of Sales All Wines = CALCULATE ( [No. of Sales], ALL ( Wines ) )
```

```
No. of Sales as Percent of Filtered Value =
DIVIDE ( [No. of Sales] , [No. of Sales All Wines] )
```

{{< figure src="./08-all-func/all-width-dim2.jpg" width=60% >}}

### 8.3. ALL với các Columns

Trong phần trên, chúng ta đã biết cách để bỏ qua các filter từ tất cả các bảng DIM hoặc từ một bảng DIM cụ thể. Giả sử bây giờ bạn muốn thu hẹp phạm vi lại, chỉ muốn loại bỏ filter trong một cột của một bảng DIM thì làm như thế nào.

```
No. of Sales All Wines #2 =
CALCULATE ( [No. of Sales] , ALL ( Wines[WINE] ) )
```

```
No. of Sales as Percent of Filtered Value #2 =
DIVIDE ( [No. of Sales] , [No. of Sales All Wines #2] )
```

{{< figure src="./08-all-func/all-with-column.jpg" width=60% >}}

### 8.4. ALLEXCEPT

Hàm ALL với các columns có thể giúp chúng ta xóa bỏ bộ lọc trên nhiều cột, nhưng trong trường hợp bạn muốn xóa bỏ bộ lọc trên rất là nhiều cột thì việc này có thể hơi mất thời gian để viết Code. Hàm ALLEXCEPT giúp chúng ta xóa bỏ bộ lọc trên tất cả các cột trong bảng được chỉ định ngoại trừ một số cột với cú pháp:

```
ALLEXCEPT ( table, column1, colum2, etc. )
```

Ví dụ:

```
ALLEXCEPT ( Wines, Wines[WINE COUNTRY] )
```

### 8.5. ALLSELECTED

{{< figure src="./08-all-func/all-selected.jpg" width=60% >}}

Một trường hợp cuối cùng khi làm việc với ALL, đó là giả sử bạn có một bảng như trên. Tình huống này chúng ta đã sử dụng hai bộ lọc của cùng một cột: `WINE` trong bảng và `WINE` trong Slicer. Vì cái cột `Grand Total` hiện đang bỏ qua bộ lọc trên bảng **Wines** nên chúng ta sử dụng Slicer sẽ không làm thay đổi giá trị trong cột này.

```
Grand Total No. of Sales = COUNTROWS ( ALL ( Winesales ) )
```

Bây giờ bạn muốn thay đổi nó, vẫn bỏ qua toàn bộ bộ lọc trong bảng nhưng ngoại trừ các giá trị trong Slicer. Đây là lúc hàm ALLSELECTED thể hiện giá trị của nó. Cú pháp:

```
ALLSELECTED ( table )
ALLSELECTED ( Column 1, Column 2, etc.)
```

Ví dụ:

```
Grand Total No. of Sales for Selected Wines =
CALCULATE ( [No. of Sales], ALLSELECTED ( Wines[WINE] ) )
```

{{< figure src="./08-all-func/allselected.jpg" width=60% >}}

Hơi khó để giải thích ý nghĩa của hàm này, mình nghĩ nó đơn giản là chỉ số được tính toán cho tất cả những giá trị được lựa chọn.

### 8.6 ALL và CALCULATE

{{< figure src="./08-all-func/all-and-calculate.jpg" width=60% >}}

```
No. of Sales = COUNTROWS( Winesales )
```

Trong phần này, chúng ta đi phân tích một số trường hợp sử dụng hàm ALL bên trong CALCULATE.

```
No. of Sales Where Cases GT 300 #1 =
CALCULATE ( [No. of Sales],
    ALL ( Winesales ), Winesales[CASES SOLD] > 350
)
```

{{< figure src="./08-all-func/all-and-calculate2.jpg" width=50% >}}

Với chỉ số đầu tiên, Hàm ALL sẽ sửa đổi bộ lọc hiện tại trên bảng **Winesales** bằng cách xóa bỏ tất cả các bộ lọc đến từ bảng **Wines**, sau đó nó áp dụng một bộ lọc mới đối với cột `CASES SOLD`.

```
No. of Sales Where Cases GT 300 #2 =
CALCULATE (
    [No. of Sales],
    FILTER (
    ALL ( Winesales ), Winesales[CASES SOLD] >350 )
)
```

{{< figure src="./08-all-func/all-and-calculate3.jpg" width=70% >}}

Với chỉ số thứ hai, Hàm ALL được sử dụng như là một hàm Table Functions để tạo bảng. Đầu tiên trong trường hợp này thì Filter vẫn được truyền từ bảng **Wines** qua bảng **Winesales**, nhưng sau đó hàm ALL đã tạo ra một bảng ảo mới bỏ qua các filter đến từ bảng **Wines**, tiếp theo là áp dụng bộ lọc đối với cột `CASES SOLD`.

Hai trường hợp này khá là dễ hiểu, nhưng trường hợp thứ 3 thì hơi phức tạp một chút.

```
No. of Sales Where Cases GT 300 #3 =
CALCULATE (
    [No. of Sales],
    ALL ( Winesales ),
    FILTER ( Winesales, Winesales[CASES SOLD] >300 )
)
```

{{< figure src="./08-all-func/all-and-calculate4.jpg" width=65% >}}

Trong chỉ số này đã sử dụng hai bộ lọc một là sử dụng hàm ALL để sửa lại filter và hai là sử dụng hàm FILTER để tạo ra một table filter. Thì lưu ý, hàm CALCULATE luôn luôn đánh giá các tham số sửa lại filter đầu tiên. Do đó, ta có:

1. Bộ lọc đầu tiên, sử dụng ALL để xóa bỏ các bộ lọc khỏi bảng **Winesales**. Cho nên chúng ta hiện có một bảng **Winesales** không có bộ lọc nào hết.
2. Bộ lọc FILTER được đánh giá độc lập với bộ lọc đầu tiên, do đó với mỗi giá trị được lọc bên trong **Wines** sẽ vẫn truyền đến hàm FILTER.
3. Hàm FILTER lặp qua các hàng trong bảng **Winesales** và tạo một bảng ảo chứa giá trị được truyền đến từ bộ lọc trong bảng **Wines**, ví dụ `Bordeaux`.
4. Cuối cùng, áp dụng điều kiện lọc trên cột `CASES SOLD` của bảng ảo, và tính toán các chỉ số cho bảng này (Bởi vì bộ lọc thứ nhất đã xóa bỏ tất cả các bộ lọc nên chúng ta không cần kết hợp nữa).

{{< admonition type=notes title="ALL Functions" open=true >}}
Cho đến nay, chúng ta đã đi qua một chẳng đường rất là dài và khó hiểu. Mình sẽ tổng hợp, sắp xếp lại các logic của FILTER, ALL và CALCULATE.

1. Khi chúng ta sử dụng Columns Filters. Đầu tiên, DAX sẽ tổng hợp các điều kiện lọc đến từ các bảng DIM, FACT. Sau đó với từng giá trị, hàm CALCULATE sẽ kết hợp với tham số filter bên trong hàm. Nếu không trùng, nó sẽ kết hợp các điều kiện với nhau. Nếu bị trùng lặp, nó sẽ ghi đè lên điều kiện lọc ban đầu.

2. Hàm FILTER là hàm được áp dụng với các bộ lọc hiện tại _(current filter context)_. Nghĩa là đầu tiên nó sẽ tổng hợp các điều kiện lọc từ các bảng DIM, FACT. Sau đó với từng nhóm, giá trị riêng lẻ nó sẽ tạo ra một cái bảng ảo riêng (Table Filters) và áp dụng các bộ lọc mới bên trong hàm FILTER. Lưu ý là FILTER không sửa đổi, ghi đè lên bộ lọc ban đầu.

3. Hàm ALL nếu sử dụng dưới dạng một Table Function, nó sẽ tạo ra một bảng ảo chứa tất cả các hàng trong một bảng nếu áp dụng với một bảng. Hoặc tất cả các hàng riêng lẻ từ một cột hoặc các cột của một bảng, nếu nó áp dụng với một tập hợp các cột. Bảng này có thể sử dụng làm tham số trong hàm FILTER để xóa bỏ các bộ lọc hiện tại.

4. Hàm ALL có thể được sử dụng như một công cụ để sửa đổi các bộ lọc hiện tại. Và nó sẽ được đánh giá đầu tiên bên trong CALCULATE. Đầu tiên, nó sẽ xóa các bộ lọc hiện tại khỏi một bảng hoặc một cột, và tạo một bộ lọc trống. các bộ lọc khác được áp dụng và tạo bộ lọc mới.

5. Hàm ALL, ALLEXCEPT, ALLSELECTED có thể giúp chúng ta loại bỏ các bộ lọc theo trình tự:

   - ALL áp dụng cho một bảng FACT, sẽ bỏ qua tất cả các bộ lọc của các bảng DIM mà liên kết với nó.
   - ALL áp dụng cho một bảng DIM, chỉ bỏ qua bộ lọc của tất cả các cột trên bảng DIM bị chỉ định.
   - ALL áp dụng cho một hoặc nhiều cột cụ thể, sẽ bỏ qua bộ lọc trên các cột này.
   - ALLEXCEPT là một cách dùng khác của hàm ALL.
   - ALLSELECTED sẽ bỏ qua bộ lọc trong một bảng hoặc một cột với những giá trị được lựa chọn trong Slicer.

{{< /admonition >}}

## 9. Empty Values vs. Zero

### 9.1. Hàm BLANK

Hàm `BLANK()` được sử dụng để trả về một giá trị null hoặc empty. Ví dụ tạo một Calculated Column:

```
10 Percent =
IF ( Winesales[CASES SOLD] > 100,
Winesales[CASES SOLD] * 0.1, BLANK () )
```

{{< figure src="./09-blank/blank.jpg" width=80% >}}

**Kiểm tra xem một giá trị có phải là BLANK**

```
Blank? =
IF ( Winesales[CASES SOLD] = BLANK(), "Blank", "Other")
```

{{< figure src="./09-blank/blank2.jpg" width=80% >}}

Như các bạn thấy thì 0 cũng là BLANK.

```
Zero? =
IF ( Winesales[CASES SOLD] = 0, "Zero", "Other")
```

Thực ra điều ngược lại cũng đúng, DAX xử lý BLANK và Zero là như nhau:

```
Zero? =
IF ( Winesales[CASES SOLD] = 0, "Zero", "Other")
```

{{< figure src="./09-blank/blank3.jpg" width=80% >}}

### 9.2. Hàm ISBLANK

Hàm ISBLANK giúp chúng ta kiểm tra xem một giá trị có chính xác là BLANK hay không. Hàm ISBLANK có phân biệt giữa BLANK và Zero:

```
Blank or Zero? =
IF (
    ISBLANK ( Winesales[CASES SOLD] ),
    "Blank",
    IF ( Winesales[CASES SOLD] = 0, "Zero", "Other" )
)
```

{{< figure src="./09-blank/isblank.jpg" width=80% >}}

### 9.3. Zero

Để xem một giá trị có chính xác là bằng 0 hay không, chúng ta sử dụng toán tử `==`:

```
Zero? =
IF (Winesales[CASES SOLD] == 0,
    "Zero",
    "Other"
)
```

### 9.4. Hàm COALESCE

Hàm COALESCE được sử dụng để tìm các giá trị BLANK (Không phải Zero), và thay thế nó bằng một giá trị mới, hai đoạn Code sau là giống nhau:

```
If Blank Return Zero =
If ( ISBLANK ( [Total Sales] ), 0, [Total Sales] )
```

```
If Blank Return Zero =
COALESCE([Total Sales],0)
```

## 10. Time Intelligence

Time Intelligence hiểu nôm na là một tập hợp của các hàm giúp chúng ta phân tích, toán toán các chỉ số theo thời gian. Ví dụ như đôi lúc bạn sẽ muốn so sánh doanh số bán hàng của tháng này so với tháng trước. Hoặc là tính tổng tích lũy theo thời gian. Nhưng trước tiên chúng ta cần phải có một bảng Date trong Data Model.

### 10.1. Date Table

Để tạo một bảng mới, chúng ta vào _Table Tools -> New Table_, sau đó chúng ta sẽ viết một số câu lệnh DAX để tạo bảng:

```
DateTable =
ADDCOLUMNS (
    CALENDARAUTO(),
    "Year", YEAR( [Date] ),
    "Month", FORMAT ( [Date], "mmmm" ),
    "Month Number", MONTH( [Date] ),
    "Quarter", FORMAT ( [Date], "\QQ" ),
    "Weekday", FORMAT ( [Date], "dddd" ),
    "Week Number", WEEKDAY( [Date] )
)
```

Sau khi tạo xong bảng **DateTable**, click chuột phải vào bảng và chọn _Mark as date table_ để Data model biết đây là bảng Dim Date.

Theo mặc định, khi các cột như `Month`, `Weekday` được đưa vào báo cáo thì nó sẽ sắp xếp các giá trị theo thứ tự của bảng chữ cái alphabet. Để thay đổi cơ chế này, hãy lựa chọn cột `Month`, sau đó vào _Column Tools -> Sort by Column -> Month Number_ để sắp xếp cột `Month` theo các giá trị của `Month Number`. Chúng ta làm tương tự đối với `Weekday`.

Hàm `CALENDARAUTO()` sẽ quét tất cả các ngày có trong các bảng và việc đó đôi khi có thể sẽ tạo ra quá là nhiều quan sát. Chúng ta có viết các công thức DAX ở mức độ chi tiết hơn:

```
DateTable =
VAR MinDate =
    YEAR ( MIN ( Winesales[SALE DATE] ) )
VAR MaxDate =
    YEAR ( MAX ( Winesales[SALE DATE] ) )
RETURN
    ADDCOLUMNS (
        FILTER (
            CALENDARAUTO (),
            YEAR ( [Date] ) >= MinDate
                && YEAR ( [Date] ) <= MaxDate
        ),
        "Year", YEAR ( [Date] ),
        "Month", FORMAT ( [Date], "mmmm" ),
        "Month Number", MONTH ( [Date] ),
        "Quarter", FORMAT ( [Date], "\QQ" ),
        "Weekday", FORMAT ( [Date], "dddd" ),
        "Week Number", WEEKDAY ( [Date] )
    )
```

**Lưu ý:** Bảng DateTime nên bao gồm dữ liệu của cả một năm, nghĩa là nó phải có đủ tất cả các ngày từ ngày `01/01` đến ngày `31/12`.

### 10.2. Functions

Các hàm Time Intelligence được tính toán dựa vào các ngày cơ sở _(base time)_. Các ngày cơ sở này được xác định dựa vào ngữ cảnh lọc hiện tại _(filter context)_. Ví dụ như là các slicer hoặc filter trong report. Các bạn cứ hiểu đơn giản là, giả sử muốn tính doanh số bán hàng một năm trước năm 2020, thì năm 2020 chính là ngày cơ sở.

{{< figure src="./10-time-intelligence/basetime.jpg" width=80% >}}

Hầu hết các hàm Time Intelligence sẽ yêu cầu một tham số ngày. Ngày này là cột chứa các giá trị ngày duy nhất bên trong **DateTable**.

{{< figure src="./10-time-intelligence/func-parameter.jpg" width=80% >}}

Thông thường, các hàm Time Intelligence sẽ tạo ra một bảng ảo chỉ có một cột được lọc từ cột tham số Date. Bảng ảo này được sử dụng làm filter bên trong hàm CALCULATE. Tuy nhiên cũng có một số hàm sẽ trả về giá trị vô hướng (Scalar) như hàm: LASTDATE, LASTNONBLANK, LASTNONBLANKVALUE. Hàm LASTDATE, LASTNONBLANK có thể được sử dụng làm filter trong hàm CALCULATE còn hàm LASTNONBLANKVALUE thì không.

### 10.3 Một số hàm đơn giản

Các hàm sử dụng trong phần này chủ yếu mang ý nghĩa so sánh:

- **PREVIOUSMONTH**: Tháng trước tính từ tháng trong filter context hiện tại.
- **SAMEPERIODLASTYEAR**: Thời gian cùng kỳ năm trước, các kỳ có thể là ngày, tháng hoặc năm,...
- **DATEADD**: Tăng hoặc giảm ngày tháng theo một đơn vị nào đó như year, quarter, month, day.
- **DATESYTD**: Trả về danh sách các ngày từ đầu năm đến filter context hiện tại.
- **DATESMTD()**: Trả về danh sách các ngày từ đầu tháng đến filter context hiện tại.
- **DATESQTD()**: Trả về danh sách các ngày từ đầu quý đến filter context hiện tại.

Chúng ta sẽ đi xây dựng một số measures với base time là tháng 12 - 2021:

{{< figure src="./10-time-intelligence/base-time.png" width=60% >}}

**Previous Month/Year**

```
Total Cases = SUM( Winesales[CASES SOLD] )
```

```
Previous Month Total Cases =
CALCULATE ( [Total Cases],
    PREVIOUSMONTH ( DateTable[DATEKEY] )
)
```

```
Previous Year Total Cases =
CALCULATE ( [Total Cases],
    PREVIOUSYEAR ( DateTable[DATEKEY] )
)
```

Hàm PREVIOUSYEAR giả định kết thúc năm tài chính là `31/12`, bạn có thể thay đổi điều đó bằng cách thêm ngày kết thúc năm tài chính vào trong hàm, ví dụ: `PREVIOUSYEAR ( DateTable[DATEKEY], "2021-03-31")`

**Same Period Last Year - Cùng kỳ năm trước**

```
Same Period Last Year Cases =
CALCULATE ( [Total Cases],
    SAMEPERIODLASTYEAR ( DateTable[DATEKEY] )
)
```

**DATEADD - Tính giá trị trong khoảng thời gian trước**

```
6 Months Ago Cases =
CALCULATE ( [Total Cases],
   DATEADD ( DateTable[DATEKEY], -6, MONTH )
)
```

```
30 Days Ago Cases =
CALCULATE ( [Total Cases] ,
     DATEADD ( DateTable[DATEKEY], -30, DAY )
)
```

**Year to Date - Từ đầu năm tài chính đến hiện tại**

```
Year To Date Cases =
CALCULATE ( [Total Cases] ,
    DATESYTD ( DateTable[DATEKEY] )
)
```

Hàm DATESYTD tương tự như PREVIOUSYEAR cũng giả định kết thúc năm tài chính là `31/12`, và bạn hoàn toàn có thể thay đổi ngày này bằng cách thêm ngày kết thúc năm tài chính vào trong hàm.

{{< figure src="./10-time-intelligence/time-intelligence.jpg" width=70% >}}

### 10.4. DATESBETWEEN & DATESINPERIOD

Các hàm trong phần này sẽ giúp chúng ta tính các chỉ số trong một khoảng thời gian nhất định:

- **DATESBETWEEN**: Trả về danh sách các ngày nằm trong khoảng thời gian.
- **DATESINPERIOD**: Trả về danh sách các ngày trong khoảng từ ngày bắt đầu đến ngày cách ngày bắt đầu một khoảng thời gian xác định, chỉ bao gồm các ngày trong filter context hiện tại. Lưu ý, nếu tham số khoảng cách là `n day` thì sẽ trả về n ngày. Nếu tham số khoảng cách là số âm thì sẽ không bao gồm giá trị mốc.
- **LASTDATE**: Trả về ngày cuối cùng trong filter context hiện tại.

**Tính tổng tích lũy theo thời gian**

```
Total Sales =
SUMX(
    Winesales,
    Winesales[CASES SOLD] * RELATED ( Wines[PRICE PER CASE] )
)
```

```
Cumulative Total =
CALCULATE ( [Total Sales] ,
    DATESBETWEEN ( DateTable[DATEKEY], 0 ,
        LASTDATE ( DateTable[DATEKEY] )
     )
)
```

{{< figure src="./10-time-intelligence/cumulative-sum.png" width=45% >}}

**Rolling Annual Totals**

```
Rolling Annual Total Sales =
CALCULATE ( [Total Sales],
    DATESINPERIOD ( DateTable[DATEKEY],
        LASTDATE ( DateTable[DATEKEY] ) , -1 , YEAR ) )
```

**Rolling Annual Averages**

```
Rolling Annual Average Total Sales =
CALCULATE (
    [Total Sales] / COUNTROWS ( VALUES ( DateTable[MONTH] ) ),
    DATESINPERIOD (
        DateTable[DATEKEY],
        LASTDATE ( DateTable[DATEKEY] ),  -1,  YEAR
    )
)
```

### 10.5. LASTNONBLANK & LASTNONBLANKVALUE

Hàm `LASTNONBLANK(<column>, <expression>)` tìm ngày cuối cùng mà `<expression>` có giá trị (không BLANK). Nếu bạn muốn xem giá trị đó là bao nhiêu thì sử dụng hàm `LASTNONBLANKVALUE(<column>, <expression>)`. Tương tự thì chúng ta cũng có hàm FIRSTNONBLANK và FIRSTNONBLANKVALUE.

```
Date of Last Transaction =
LASTNONBLANK ( DateTable[DATEKEY], [Total Sales] )
```

```
Value of Last Transaction =
LASTNONBLANKVALUE ( DateTable[DATEKEY], [Total Sales] )
```

{{< figure src="./10-time-intelligence/lastnonblank.jpg" width=70% >}}

## 11. More about Filter

### 11.1. SELECTEDVALUE & CONCATENATEX

Giả sử có một slicer, và trong slicer đó có một số giá trị được lựa chọn. Trong phần này, chúng ta sẽ tìm hiểu một số hàm để giúp chúng ta lấy ra các giá trị được lựa chọn này.

Hàm `SELECTEDVALUE(<ColumnName>, <AlternateResult>)` sẽ trả về cho chúng ta một giá trị từ filter nếu cái filter đó chỉ lọc ra một giá trị duy nhất, ví dụ như khi bạn chỉ chọn một giá trị trong slicer. Ngược lại hàm sẽ trả về giá trị ở tham số `AlternateResult`.

Ví dụ:

```
Wine Selected =
"You have selected " & SELECTEDVALUE ( Wines[WINE] )
```

Áp dụng, giả sử ta có một bảng như sau:

{{< figure src="./11-more-filter/filter-start.jpg" width=55% >}}

Chúng ta sẽ tạo một Card visual với chỉ số vừa tạo ở trên, và ta có kết quả:

{{< figure src="./11-more-filter/card-visual.png" width=65% >}}

Như đã nói thì hàm SELECTEDVALUE chỉ có thể trả về một giá trị được lựa chọn duy nhất, bây giờ nếu bạn lựa chọn nhiều giá tị trong Slicer thì làm sao để có thể lấy được các giá trị đó. Đầu tiên chúng ta làm quen với hàm CONCATENATEX. Hàm này giúp nối các nội dung trong cùng một cột của một bảng thành một chuỗi ký tự. Hàm CONCATENATEX phụ thuộc vào filter context hiện tại.

```
CONCATENATEX( table, expression, delimiter, order by, order )
```

Trong đó:

- **table**: Bảng chứa cột có nội dung cần nối.
- **expression**: Biểu thức trả về một cột có chứa nội dung cần nối.
- **delimiter**: Ký tự dùng để nối các nội dung, nếu không nhập thì các nội dung sẽ được nối liền nhau.
- **order by**: Cột được sử dụng làm căn cứ sắp xếp thứ tự kết nối.
- **order**: Sắp xếp theo thứ tự các chữ cái tăng dần _(ASC - mặc định)_ hoặc giảm dần _(DESC)_

Áp dụng lại hàm CONCATENATEX với ví dụ trên:

```
Types of Wine =
CONCATENATEX ( Wines, Wines[WINE], ", " )
```

{{< figure src="./11-more-filter/card-visual2.png" width=65% >}}

Tuy nhiên, nếu bạn không chọn giá trị nào, tất cả các giá trị sẽ được hiển thị:

{{< figure src="./11-more-filter/card-visual3.png" width=65% >}}

Bây giờ, ta sẽ viết lại biểu thức DAX trên cho các tình huống sẽ gặp phải:

- Không có giá trị nào được lựa chọn trong slicer
- Có ba giá trị được lựa chọn hoặc ít hơn.
- Có nhiều hơn ba giá trị được lựa chọn.

Trước tiên chúng ta sẽ làm quen với hàm VALUES. Hàm này khi áp dụng với một cột, nó sẽ tạo ra một bảng ảo chỉ gồm một cột và các giá trị trong cột này là duy nhất. Lưu ý là hàm VALUES phụ thuộc vào filter context hiện tại.

```
Types of Wine =
VAR NoFilteredWines =
    COUNTROWS ( VALUES ( Wines[WINE] ) )
VAR NoAllWines =
    COUNTROWS ( ALL ( Wines[WINE] ) )
RETURN
    IF (
        NoFilteredWines = NoAllWines,
        "Sales by Wine",
        "Sales by Wine, filtered by " & CONCATENATEX ( Wines, Wines[WINE], ", " )
    )
```

Đoạn code này sẽ hiển thị `Sales by Wine` nếu không có giá trị nào được lựa chọn, ngược lại sẽ hiển thị danh sách các giá trị được lựa chọn.

Tiếp theo chúng ta sẽ sử dụng thêm hàm TOPN để giải quyết 2 vấn đề còn lại. Hàm TOPN sẽ tạo ra một cột mới gồm N giá trị đầu tiên từ cột được chỉ định.

```
Types of Wine =
VAR NoFilteredWines =
    COUNTROWS ( VALUES ( Wines[WINE] ) )
VAR NoAllWines =
    COUNTROWS ( ALL ( Wines[WINE] ) )
RETURN
    IF (
        NoFilteredWines = NoAllWines,
        "Sales by Wine",
        "Sales by Wine, filtered by "
            & IF (
                NoFilteredWines <= 3,
                CONCATENATEX ( Wines, Wines[WINE], ", " ),
                CONCATENATEX ( TOPN ( 3, VALUES ( Wines[WINE] ) ), Wines[WINE], ", " ) & " and more..."
            )
    )
```

### 11.2. Parameter Tables

Tham số bảng, hiểu đơn giản là chúng ta có thể tạo một bảng làm tham số sử dụng cho một hàm. Ví dụ chúng ta tạo một bảng **What If** như sau:

{{< figure src="./11-more-filter/table-parameters.jpg" width=65% >}}

Bây giờ ta sẽ đi tạo một chỉ số để tính toán dựa vào giá trị được chọn trong slicer.

```
What If Scenario =
[Total Sales] * SELECTEDVALUE ( 'What If'[Value] )
```

{{< figure src="./11-more-filter/table-parameters2.jpg" width=65% >}}

Một ví dụ nữa sử dụng tham số bảng, để lựa chọn chỉ số tính toán từ một slicer.

Ta tạo một bảng như sau:

{{< figure src="./11-more-filter/table-parameters3.jpg" width=65% >}}

```
MEASURE To Show =
    SWITCH (
        SELECTEDVALUE ( 'Select Measures'[Value] ),
        1, [Total Sales],
        2, [Total Cases],
        3, [No. of Sales]
    )
```

Kết quả:

{{< figure src="./11-more-filter/table-parameters4.jpg" width=65% >}}

### 11.3. Hàm VALUES

Cú pháp:

```
VALUES ( table name or column name )
```

Trong đó:

- **table name:** Khi tham số là một bảng, nó sẽ trả về một bảng gồm các hàng từ bảng được chỉ định sau khi đã lọc theo filter context hiện tại.
- **column name:** Khi tham số là một cột nó sẽ trả về một bảng chỉ có một cột, gồm các giá trị khác nhau từ cột được chỉ định dựa vào filter context hiện tại.

Khi làm việc với hàm VALUES, có thể chúng ta sẽ kết hợp với hàm `HASONEVALUE(column)`, để kiểm tra xem trong một cột có một hay nhiều giá trị, nếu có một giá trị nó sẽ trả về `True`. Hàm này cũng phụ thuộc vào filter context hiện tại.

Ví dụ, hai code dưới đây là tương đương nhau:

```
Values Wine =
IF ( HASONEVALUE ( Wines[WINE] ), VALUES ( Wines[WINE] ), "All Wines" )
```

```
Selected Value Wine =
SELECTEDVALUE ( Wines[WINE], "All Wines" )
```

### 11.4. Filter Propagation

Cho đến nay, chúng ta mới chỉ làm việc với các bộ lọc đi từ bảng DIM đến bảng FACT, đi từ phía _one side_ đến _many side_.

{{< figure src="./11-more-filter/filter-propagation.jpg" width=80% >}}

Tuy nhiên, trong một số trường hợp bạn sẽ muốn truyền dữ liệu ngược lại với chiều được xác định trong Data Model. Như đã nói trước đó, chúng ta sẽ không thay đổi trên Data Model mà sử dụng một hàm khác để thay đổi chiều, đó là hàm CROSSFILTER.

Nhớ lại một ví dụ trước đó, chúng ta muốn tính tổng số cửa hàng đang bán mỗi loại rượu:

{{< figure src="./11-more-filter/filter-propagation3.jpg" width=45% >}}

{{< figure src="./11-more-filter/filter-propagation2.jpg" width=80% >}}

Như các bạn thấy thì filter direction không cho phép chúng ta lấy thông tin từ bảng **Customers**. Bây giờ chúng ta sẽ đi tìm hiểu về hàm CROSSFILTER:

```
CROSSFILTER ( column1, column2, direction )
```

Trong đó:

- **column1**: Tên cột khóa của bảng phía many của mối quan hệ.
- **column2**: Tên cột khóa của bảng phía one của mối quan hệ.
- **direction**: single hoặc both.

Ví dụ:

```
Total Stores =
CALCULATE (
    SUM ( Customers[NO. OF STORES] ),
    CROSSFILTER ( Winesales[CUSTOMER ID], Customers[CUSTOMER ID], BOTH )
)
```

### 11.5. Multiple Relationships

Đôi khi, bạn sẽ gặp một số tình huống mà giữa hai bảng có nhiều mối quan hệ, tuy nhiên tại một thời điểm chỉ có một mối quan hệ duy nhất được hoạt động. Ví dụ:

{{< figure src="./11-more-filter/multi-relationships.jpg" width=55% >}}

Trong trường hợp, bạn muốn sử dụng một mối quan hệ không được kích hoạt, các bạn có thể sử dụng hàm USERELATIONSHIP, tương tự như CROSSFILTER. Cú pháp:

```
USERELATIONSHIP ( column1, column2 )
```

## 12. Context Transition

Khi học về DAX, một trong những kiến thức nền tảng quan trọng nhất bạn phải nắm được là _Evaluation Context_, có nghĩa là bạn phải hiểu được các loại ngữ cảnh và những tình huống khi mà một ngữ cảnh bị chuyển đổi thành ngữ cảnh khác. Trước khi đi tìm hiểu về Context Transition, chúng ta ôn tập lại hai loại ngữ cảnh đã được nhắc đến trong phần Calculated Columns và Measures: Row Context và Filter Context.

Giả sử trong bảng **Winesales**, chúng ta sẽ tạo ra một Calculated Column với nội dung:

```
10 Percent of Cases Sold = Winesales[CASES SOLD] * 0.1
```

Với Row Context, đầu tiên DAX sẽ lặp qua từng hàng bên trong bảng **Winesales**, tìm ra giá trị tương ứng của `CASES SOLD` trong hàng đó và nhân với `0.1`. Các bạn có thể nghĩ về Row Context giống như các phép tính trong một ô _(Cell)_ của Excel, sau đó bạn kéo công thức tính của ô đó xuống các ô bên dưới trong cùng một cột để thực hiện các phép tính tương tự.

Khi nhắc về Filter Context, về cơ bản tất cả các biểu thức DAX đều được tính toán dựa trên ba bước sau:

- **Bước 1**: Xác định các bộ lọc từ slicer, từ reports và visual,...sau đó thực hiện lọc dữ liệu để có một bảng dữ liệu mới.
- **Bước 2**: Tính toán các chỉ số dựa vào bảng dữ liệu mới này.
- **Bước 3**: Gửi kết quả tính toán được trở lại slicer, reports, table.

Một ví dụ về Filter Context kết hợp với Row Context, chúng ta tạo ra chỉ số `Total Sales`:

```
Total Sales =
SUMX ( Winesales,
    Winesales[CASES SOLD] * RELATED ( Wines[PRICE PER CASE] )
)
```

Ví dụ này có thể được phân tích thành các bước sau:

- Bước 1: Xác định các bộ lọc và gửi đến bảng **Winesales** để lọc dữ liệu _(Filter Context)_.
- Bước 2: Dựa trên dữ liệu đã được lọc, tạo ra một cột calculated column ảo _(cái này để hình dung)_ tính toán `Winesales[CASES SOLD] * RELATED ( Wines[PRICE PER CASE] )` _(Row Context)_.
- Bước 3: Tính tổng tất cả các giá trị trong cột ảo vừa tạo và gửi giá trị đó đến reports.

Để nói về Context Transition, về mặt ý nghĩa nó chỉ đơn giản là trong một số tình huống Row Context sẽ bị chuyển đổi thành Filter Context hoặc ngược lại. Và chúng ta sẽ đi xem xét từng tình huống đó.

### 12.1. Calculated Columns

Có hai quy tắc chúng ta cần phải nhớ:

- Thứ nhất, các chỉ số luôn luôn ngầm gọi hàm CALCULATE, cho dù chúng ta có sử dụng hay không.
- Thứ hai, khi hàm CALCULATE được sử dụng thì sẽ xảy ra Context Transition, Row Context sẽ bị chuyển thành Filter Context.

Để giải thích cho trường hợp, mình sẽ minh họa bằng một số ví dụ sau. Chúng ta bắt đầu với một Calculated Column trong bảng **Winesales**.

```
Total Cases Column =
SUM ( Winesales[CASES SOLD] )
```

Như các bạn sẽ thấy thì, biểu thức này sử dụng Row Context lặp qua từng hàng của bảng dữ liệu sau đó tính tổng tất cả các giá trị bên trong cột `CASES SOLD` vì Filter Context bây giờ được ngầm hiểu là toàn bộ bảng dữ liệu. Do đó tất cả các hàng đều có cùng một giá trị.

{{< figure src="./12-context-transition/calculated-column.jpg" width=80% >}}

Bây giờ chúng ta thử sửa đổi biểu thức DAX trên thành:

```
Total Cases Column =
CALCULATE (
    SUM ( Winesales[CASES SOLD] )
)
```

{{< figure src="./12-context-transition/calculated-column2.jpg" width=80% >}}

Như bạn thấy, bây giờ giá trị trong các hàng không còn giống nhau nữa. Khi ta sử dụng hàm CALCULATE mà không có đối số filter thì DAX sẽ sử dụng một tập hợp các giá trị trong tất tất cả các cột còn lại làm filter. Ví dụ với giá trị `213` của `Total Cases Column`, sẽ được tính toán với bộ filter sau:

```
SALE DATE = 01/01/2017
WINESALES NO = 2
SALESPERSON ID = 6
CUSTOMER ID = 16
WINE ID = 10
CASES SOLD  = 213
```

Tương tự, kết quả cũng giống như trên khi chúng ta có thay thế hàm CALCULATE ở trên bằng một chỉ số:

```
Total Cases =
SUM ( Winesales[CASES SOLD] )
```

```
Total Cases Column =
[Total Cases]
```

Một ví dụ nữa, thay vì tính toán trên bảng Fact, bây giờ chúng ta tính toán trên bảng Dim **Wines**:

```
Wine Total Cases 1 = SUM ( Winesales[CASES SOLD] )
```

```
Wine Total Cases 2 =
CALCULATE (
    SUM ( Winesales[CASES SOLD] ) )
```

```
Wine Total Cases 3 = [Total Cases]
```

{{< figure src="./12-context-transition/calculated-column3.jpg" width=80% >}}

Trong phần này, chúng ta đã xem một số ví dụ về Context Transition sử dụng Calculated Column, tuy nhiên thực thì chúng ta sẽ chủ yếu sử dụng các biểu thức DAX khi xây dựng các chỉ số (Measures). Và hoạt động Context Transition bên trong các chỉ số sẽ phức tạp và khó hiểu hơn rất nhiều, nhất là khi chúng ta lồng các chỉ số bên trong biểu thức DAX.

### 12.2. AVERAGE làm Filters

Chúng ta sẽ bắt đầu với hai chỉ số tổng số đơn hàng bán được `No. of Sales` và số lượng hàng trung bình một đơn hàng bán được `Avg Cases`:

```
No. of Sales = COUNTROWS ( Winesales )
Avg Cases = AVERAGE ( Winesales[CASES SOLD] )
```

{{< figure src="./12-context-transition/filter-using-average.png" width=50% >}}

Như trong hình, ví dụ có 180 đơn hàng bán `Bordeaux` và trung bình mỗi đơn hàng bán được khoảng 300 chai. Giả sử bây giờ bạn muốn tìm tổng những đơn hàng mà có số lượng bán `Borrdeaux` lớn hơn 300. Tương tự với những loại rượu vang khác.

```
No. Of Sales GT Avg =
VAR AvgCasesTable =
    FILTER ( Winesales, Winesales[CASES SOLD] > [Avg Cases] )
RETURN
    CALCULATE ( [No. Of Sales], AvgCasesTable )
```

Kết quả:

{{< figure src="./12-context-transition/filter-using-average2.png" width=40% >}}

Kết quả nhận được là không có gì hết, rõ ràng chúng ta đã viết đúng công thức rồi, tại sao lại như vậy nhỉ. Để giải thích cho tình huống này, chúng ta cần nhớ rằng khi nghĩ về DAX chúng ta hãy nghĩ về các cột, hàng và bảng thay vì nghĩ về từng ô. Điều đó có nghĩa là `Winesales[CASES SOLD]` là một cột và `[Avg Cases]` cũng là một cột, hàm FILTER sẽ lặp qua từng hàng trong bảng **Winesales** để tìm các hàng thỏa mãn điều kiện.

Ở trên chúng ta đã nói, khi sử dụng một measure thì Context Transition sẽ xảy ra. Do đó trong trường hợp này `CASE SOLD` luôn bằng với `Avg Cases`:

{{< figure src="./12-context-transition/filter-using-average3.png" width=80% >}}

Bây giờ chúng ta sửa lại biểu thức DAX trên:

```
No. Of Sales GT Avg =
VAR AvgCasesTable =
    FILTER ( Winesales, Winesales[CASES SOLD] > AVERAGE ( Winesales[CASES SOLD] ) )
RETURN
    CALCULATE ( [No. Of Sales], AvgCasesTable )
```

{{< figure src="./12-context-transition/filter-using-average4.png" width=80% >}}

Và chúng ta có kết quả chính xác:

{{< figure src="./12-context-transition/filter-using-average5.png" width=40% >}}

### 12.3. MAX làm Filters

Chúng ta sẽ tiếp tục với một ví dụ nữa, lần này chúng ta đi tính tổng tích lũy theo thời gian.

```
Cumulative Total =
VAR FilteredDatesTable =
    FILTER ( ALL ( DateTable ), DateTable[DATEKEY] <= MAX ( DateTable[DATEKEY] ) )
RETURN
    CALCULATE ( [Total Sales], FilteredDatesTable )
```

Chúng ta đã sử dụng hàm ALL để xóa các bộ lọc hiện tại và hàm FILTER để tạo ra một bảng ảo mới. Nếu ở đây bạn thay `MAX ( DateTable[DATEKEY] )` thành một chỉ số, kết quả sẽ không như mong muốn.

```
Max Date =
MAX ( DateTable[DATEKEY] )
```

```
Cumulative Total Wrong =
VAR FilteredDatesTable =
    FILTER ( ALL ( DateTable ), DateTable[DATEKEY] <= [Max Date] )
RETURN
    CALCULATE ( [Total Sales], FilteredDatesTable )
```

{{< figure src="./12-context-transition/filter-using-max.jpg" width=50% >}}

### 12.4. Measures làm Filters

Với hai ví dụ trên, chúng ta đã gặp vấn đề khi sử dụng các chỉ số làm filter, vậy thì các chỉ số có thể được sử dụng làm filter hay không, câu trả lời là có. Chúng ta sẽ minh họa cho điều này bằng ví dụ tính tổng số đơn hàng có doanh thu lớn hơn `10,000`.

```
No. Of Sales GT 10,000 =
VAR MySales =
    SUMX ( Winesales, Winesales[CASES SOLD] *
                  RELATED ( Wines[PRICE PER CASE] ) )
VAR SalesTable =
    FILTER ( Winesales, MySales > 10000 )
RETURN
    CALCULATE ( [No. Of Sales], SalesTable )
```

Nếu bạn sử dụng biểu thức DAX này sẽ gặp lỗi, vì MySales sẽ hoạt động như Calculated Column và kết quả của tất cả các hàng đều giống nhau:

{{< figure src="./12-context-transition/filter-using-measures.jpg" width=80% >}}

Do đó chúng ta cần sửa lại biểu thức trên một chút:

```
Total Sales =
SUMX ( Winesales, Winesales[CASES SOLD] *
                  RELATED ( Wines[PRICE PER CASE] )
```

```
No. Of Sales GT 10,000 =
VAR SalesTable =
    FILTER ( Winesales, [Total Sales] > 10000 )
RETURN
    CALCULATE ( [No. Of Sales], SalesTable )
```

### 12.5. Tổng hợp dữ liệu theo bảng DIM

Giả sử chúng ta có một bảng tổng hợp dữ liệu như sau và chúng ta muốn đi tìm giá trị lớn nhất trong cột `Total Cases`:

```
Max Cases = MAX ( Winesales[CASES SOLD] )
Total Cases = SUM ( Winesales[CASES SOLD] )
```

{{< figure src="./12-context-transition/aggregate1.jpg" width=50% >}}

```
Max of Totals =
MAXX (
    ALL ( Wines ) , [Total Cases] )
```

Nếu bạn không sử dụng ALL để xóa bộ lọc, nó sẽ trả về giá trị tương tự như `Total Cases`. Biểu thức sau sẽ tìm loại rượu có tổng số lượng bán lớn nhất:

```
Wine with Max =
VAR MyMax =
    MAXX ( ALL ( Wines ), [Total Cases] )
RETURN
    CALCULATE ( VALUES ( Wines[WINE] ), FILTER ( Wines, [Total Cases] = MyMax ) )
```

{{< figure src="./12-context-transition/aggregate2.jpg" width=60% >}}

### 12.6. Hàm SUMMARIZE

Hàm ALL có thể tạo ra một bảng ảo gồm một hoặc nhiều cột từ một bảng nào đó. Nhưng nếu bạn muốn tạo ra một bảng kết hợp các cột đến từ nhiều bảng, chúng ta sẽ phải sử dụng hàm SUMMARIZE. Cú pháp:

```
SUMMARIZE ( table, group by column1, group by column2 etc., name, expression )
```

Trong đó:

- **table**: Bảng hoặc biểu thức trả về bảng có chứa các cột mà bạn muốn tổng hợp dữ liệu.
- **group by column**: Các cột mà bạn muốn tổng hợp dữ liệu, có thể cùng bảng hoặc các bảng khác có liên kết.
- **name**: Tên của cột chỉ số mà bạn sẽ tạo ra.
- **expression**: Biểu thức tổng hợp dữ liệu.

Ví dụ, tạo một bảng mới _Table tools -> New Table_ với biểu thức sau:

```
Wine and Year Table =
SUMMARIZE ( Winesales,
   Wines[WINE], DateTable[YEAR] )
```

**Lưu ý:** Tuy cả SUMMARIZE và ALL đểu được sử dụng để tạo ra một bảng ảo kết hợp dữ liệu từ nhiều cột, tuy nhiên ALL loại bỏ filter context hiện tại, còn SUMMARIZE sẽ phụ thuộc vào filter context hiện tại.

### 12.7. Hàm RANKX

Hàm RANKX được sử dụng để xếp hạng dữ liệu theo một chỉ số nào đó.

```
RANKX ( table, expression, value, order, ties )
```

Trong đó:

- **table**: Bảng được sử dụng để xếp hạng.
- **expression**: Chỉ số dùng để xếp hạng các hàng trong bảng trên.
- **order**: Mặc định là DESC (1 là hạng cao nhất), ASC (1 là hạng thấp nhất).
- **ties**: _Skip_ - Các giá trị bằng nhau cùng hạng, sau đó bị bỏ qua (ví dụ 1, 2, 2, 2, 5,...). _Dense_ - Các giá trị bằng nhau cùng hạng, số hạng tiếp theo tiếp tục số hạng trước đó (ví dụ 1, 2, 2, 2, 3, 4,...).

Ví dụ:

```
RANKX ( ALL (Wines), [Total Sales],, DESC)
```

Ứng dụng hàm RANK để xếp hạng tổng doanh số bán hàng theo từng quý.

```
Rank by Qtr =
 IF ( HASONEVALUE(DateTable[Quarter] ),
      RANKX ( ALL ( DateTable[Quarter] ), [Total Cases] ))
```

{{< figure src="./12-context-transition/rankx.png" width=40% >}}

### 12.8. Ví dụ

Mỗi một nhân viên bán hàng đều có một danh sách các khách hàng khác nhau. Bây giờ chúng ta sẽ sử dụng tổng hợp những kiến thức từ đầu bài viết cho đến nay để xây dựng một chỉ số đi tìm kiếm những khách hàng mang lại TOP `n%` hoặc BOTTOM `n%` tổng doanh thu. Chúng ta sẽ có ba slicer:

- Top or Bottom: Để lựa chọn xem là tìm kiếm Top hoặc Bottom.
- Percent: Số lượng khách hàng muốn tìm kiếm.
- Sales: Danh sách nhân viên bán hàng.

Đầu tiên chúng ta đi tạo hai bảng như hình:

{{< figure src="./12-context-transition/create-table.jpg" width=70% >}}

Sau đó, chúng ta tạo những bảng cần thiết để có một cái nhìn tổng quan.

{{< figure src="./12-context-transition/examp.png" width=70% >}}

Như các bạn thấy thì bây giờ chúng ta còn thiếu một chỉ số để đi tìm kiếm các khách hàng thỏa mãn các filter đến từ slicer.

```
Top/Bottom PC Customers =
VAR PercentToFind =
    COUNTROWS ( ALL ( Customers ) ) * SELECTEDVALUE ( 'Select Percent'[Percent] ) -- Harvest the percent using the slicer selection

VAR RankCustsTop =
    RANKX ( ALL ( Customers ), [Total Sales],, DESC ) -- Rank the customers descending by Total Sales value (Top = 1)
VAR FindCustsTop =
    FILTER ( Customers, RankCustsTop <= PercentToFind ) -- Filter top customers whose rank is less than or equal to the PerCentToFind
VAR CalcSalesTop =
    CALCULATE ( [Total Sales], FindCustsTop ) -- Calculate “Total Sales” for top ranked customers

VAR RankCustsBottom =
    RANKX (
        FILTER ( ALL ( Customers ), NOT ( ISBLANK ( [Total Sales] ) ) ),
        [Total Sales],
        ,
        ASC
    ) -- Rank the customers ascending by Total Sales value (Bottom = 1) but only if they have sales
VAR FindCustsBottom =
    FILTER ( Customers, RankCustsBottom <= PercentToFind ) -- Filter bottom customers whose rank is less than or equal to the PerCentToFind
VAR CalcSalesBottom =
    CALCULATE ( [Total Sales], FindCustsBottom ) -- Calculate “Total Sales” for bottom ranked customers

VAR TopOrBottom =
    SELECTEDVALUE ( 'Select Top or Bottom'[Top or Bottom] ) -- Harvest whether top or bottom using the slicer selection

RETURN
    IF (
        HASONEVALUE ( Customers[CUSTOMER NAME] ),
        -- This tests that the evaluation is not for the Total Row.
        IF (
            TopOrBottom = "top",
            CalcSalesTop,
            CalcSalesBottom
        ),
        --The calculation for rows not in the Total row
        CALCULATE (
            [Total Sales],
            ALLSELECTED ( Customers[CUSTOMER NAME] )
        )
    )
```

## 13. Virtual Relationships

Đôi khi vì một lý do nào đó, bạn không thể tạo được mối liên kết giữa các bảng dữ liệu với nhau. Khi đó chúng ta cần sử dụng một số hàm để tìm kiếm các giá trị dựa vào một điều kiện nào đó hoặc là tạo các mối liên kết ảo.

### 13.1. Hàm LOOKUPVALUE

Trong Phần 2 về _[Calculated Column](#2-calculated-column)_, mình đã trình bày về hàm RELATED. Hàm này giúp chúng ta lấy các giá trị từ bảng One đến bảng Many trong mối quan hệ One-to-Many. Nó hoạt động tương tự như hàm VLOOKUP trong Excel, tuy nhiên bạn chỉ có thể sử dụng hàm RELATED khi các bảng đã được liên kết với nhau dựa vào mối quan hệ One-to-Many.

Giả sử bây giờ, với mỗi loại rượu trong bảng **Wines** sẽ được bán ở các mức giá khác nhau tùy thuộc vào số lượng mua hàng. Ví dụ như bảng **Prices** trong file [dữ liệu](./data/4%20DAX%20LOOKUPVALUE.pbix) :

{{< figure src="./13-virtual-relationships/prices.jpg" width=60% >}}

Khi này, trong bảng **Winesales** cũng được thêm một cột `PRICE BAND`:

{{< figure src="./13-virtual-relationships/winesales.jpg" width=80% >}}

Và mối quan hệ giữa các bảng:

{{< figure src="./13-virtual-relationships/data-model.png" width=80% >}}

Như các bạn thấy thì trong trường hợp này, chúng ta không thể sử dụng hàm RELATED để lấy giá của các loại rượu từ bảng **Prices**. Hàm LOOKUPVALUE sẽ giúp ta làm điều đó. Cú pháp:

```
LOOKUPVALUE( result column name, search column name1, search value1, search column name2, search value2 etc. )
```

Trong đó:

- **result column name**: Tên của cột giá trị chứa kết quả mà bạn muốn tìm kiếm.
- **search column name**: Cột chứa giá trị cần tìm, cùng bảng với cột kết quả.
- **search value**: Cột giá trị tìm kiếm, thường nằm ở một bảng khác.

Các bạn có thể nghĩ `search column name` và `search value` như là các cột khóa giữa hai bảng. Ví dụ:

```
WINE PRICE =
LOOKUPVALUE (
    Prices[PRICE PER CASE],
    Prices[WINE ID], Winesales[WINE ID],
    Prices[PRICE BAND], Winesales[PRICE BAND]
)
```

Một cách viết khác của biểu thức trên:

```
WINE PRICE =
VAR currentwine = Winesales[WINE ID]
VAR priceband = Winesales[PRICE BAND]
RETURN
CALCULATE ( VALUES ( Prices[PRICE PER CASE] ),
        Prices[PRICE BAND] = priceband,
        Prices[WINE ID] = currentwine )
```

### 13.2. Hàm TREATAS

Giả sử bây giờ mỗi nhân viên bán hàng, đều được yêu cầu có một mục tiêu bán hàng hàng năm như bảng **Targets** trong [Data Model](./data/5%20DAX%20TREATAS.pbix) như sau:

{{< figure src="./13-virtual-relationships/target.jpg" width=40% >}}

{{< figure src="./13-virtual-relationships/data-model2.png" width=60% >}}

Và chúng ta muốn so sánh tổng doanh thu mà mỗi nhân viên mang về cho công ty so với mục tiêu đề ra trong từng năm. Trước tiên ta cần 2 chỉ số:

```
Target = SUM ( Targets[TARGET] )
Total Sales = SUMX( Winesales , Winesales[CASES SOLD] * RELATED( Wines[PRICE PER CASE]) )
```

Bây giờ có một vấn đề, chúng ta sẽ lấy `YEAR` từ bảng nào.

{{< figure src="./13-virtual-relationships/target2.jpg" width=80% >}}

Nếu mà chúng ta lấy `YEAR` từ bảng **DataTable** thì chỉ số `Target` sẽ không chính xác, ngược lại nếu chúng ta lấy `YEAR` từ bảng **Targets** thì chỉ số `Total Sales` lại không chính xác.

{{< figure src="./13-virtual-relationships/data-model3.png" width=60% >}}

Như trong Data Model, nếu chúng ta lấy `YEAR` từ bảng **DataTable** thì thông tin không thể truyền đến được bảng **Targets** và ngược lại. Có thể bạn sẽ nghĩ là tạo mối liên kết giữa hai bảng **DataTable** và **Target**, tuy nhiên ở đây chúng ta sẽ gặp phải mối quan hệ Many-to-Many. May mắn là, DAX có một hàm có thể giúp chúng ta giải quyết vấn đề này, đó là hàm TREATAS. Cú pháp:

```
TREATAS ( table expression, column1, column2 etc. )
```

Trong đó:

- **table expression**: Là bất kỳ biểu thức nào trả về một bảng.
- **column**: Một hoặc nhiều cột dùng để tạo liên kết.

Và bây giờ, Target có thể được viết lại như sau:

```
Target =
CALCULATE (
    SUM ( Targets[TARGET] ),
    TREATAS ( VALUES ( DateTable[YEAR] ), Targets[YEAR] )
)
```

{{< figure src="./13-virtual-relationships/data-model4.png" width=60% >}}

Các bạn có thể hình dung về hàm TREATAS đơn giản như sau:

- Đầu tiên TREATAS sử dụng hàm VALUES để tạo một bảng ảo chỉ có một giá trị từ bảng **DataTable**, bởi vì filter context chỉ có một giá trị, giả sử là năm 2017.
- Sau đó, thông tin này được truyền cho bảng **Target** để lọc các dữ liệu tính toán cho hàm CALCULATE.

{{< figure src="./13-virtual-relationships/target3.jpg" width=50% >}}

## 14. Table Expansion

## 15. Tài liệu tham khảo

Bài viết này, mình tổng hợp lại các kiến thức dựa trên quyển sách _[Up and Running with DAX for Power BI : A Concise Guide for Non-Technical Users](https://learning.oreilly.com/library/view/up-and-running/9781484281888/)_ của _Alison Box_.
