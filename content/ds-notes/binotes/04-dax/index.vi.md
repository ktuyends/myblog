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

Time Intelligence hiểu nôm na là một tập hợp của các hàm giúp chúng ta phân tích, toán toán các chỉ số theo thời gian. Ví dụ như đôi lúc bạn sẽ muốn so sánh doanh số bán hàng của tháng này so với tháng trước. Hoặc là tính tổng tích lũy theo thời gian.

### 10.1. Date Hierarchies

### 10.2. Date Table

### 10.3. Một số hàm DateTime

## 11. More about Filter

## 12. Context Transition

## 13. Virtual Relationships

## 14. Table Expansion
