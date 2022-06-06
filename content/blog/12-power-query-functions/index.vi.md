---
title: "Parameters và Custom Function trong Power Query"
subtitle: ""
slug: power-query-custom-function
summary: ""
date: 2022-06-06
lastmod: 2022-06-06
draft: false
authors: ["Tuyen Kieu"]
images: ["featured.png"]
tags: ["Blog", "Power Query"]
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

Power Query sử dụng ngôn ngữ M để xây dựng các quy trình _(steps)_ biến đổi và chuẩn bị dữ liệu. Nói theo một cách khác, thì Power Query là giao diện trực quan giúp chúng ta tạo ra các đoạn M Code với mỗi thao tác mà chúng ta thực hiện, tương tự như Macro trong Excel sẽ tạo ra các đoạn code VBA trong quá trình ghi macro.

Hầu hết thời điểm có lẽ chúng ta chỉ cần sử dụng những gì được xây dựng sẵn trong Power Query là đủ, nhưng trong một số tình huống phức tạp, đòi hỏi ta phải chỉnh sửa lại M Code hoặc viết lại hoàn toàn từ đầu. Trong bài viết này, mình viết về _Parameters_ và _Custom Functions._ Đây là hai công cụ có thể sẽ giúp ích khá nhiều cho việc tự động hóa các bước chuẩn bị dữ liệu của chúng ta.

## 1. Parameters

Đầu tiên, từ trên tab _Home_ của thanh Ribbon, ta click vào _Enter Data_ và tạo một bảng đơn giản như sau:

{{< figure src="./parameters.png" width=85% >}}

Bây giờ, chúng ta sẽ chọn _Keep Top Rows_ để lấy 2 dòng đầu tiên trong bảng:

{{< figure src="./parameters2.png" width=85% >}}

Như bạn thấy, Power Query đã giúp chúng ta tạo ra một đoạn M Code như này:

```
= Table.FirstN(Source,2)
```

Power Query sử dụng một hàm được gọi là `Table.FirstN` với hai tham số để lấy hai dòng đầu tiên trong bảng:

- _Table_: Tên của bảng hoặc truy vấn tương ứng trả về kiểu dữ liệu `table`.
- _countOrCondition_: Số dòng mà bạn muốn lấy, trong ví dụ trên là 2.

Bạn cũng có thể xem thông tin về một hàm bằng cách nhập tên của hàm đó vào trong ô formula:

{{< figure src="./parameters3.png" >}}

Quay lại với ví dụ trên, chúng ta hoàn toàn có thể thay thế giá trị `2` ở trong công thức `Table.FirstN(Source,2)` bằng một tham số _(parameter)_ mà khi ta thay đổi giá trị của tham số thì kết quả của _query step_ cũng sẽ thay đổi theo.

Để tạo một tham số, từ tab _Home_ của thanh Ribbon, ta vào _Manage Parameters -> New Parameter_, nhập tên tham số, kiểu dữ liệu và các giá trị tương ứng của tham số, sau đó click vào OK để hoàn tất.

{{< figure src="./parameters4.png" width=55% >}}

Đến đây, bạn có thể thay thế tham số vừa tạo vào trong hàm `Table.FirstN` như sau:

```
= Table.FirstN(Source, Keep_top_n)
```

Bây giờ, bạn thử thay đổi giá trị của tham số, sau đó quay trở lại query step để xem kết quả đã thay đổi.

Trên thực tế, ta cũng có thể sử dụng các queries như một tham số nếu query đó có kiểu dữ liệu tương ứng với kiểu dữ liệu của tham số được định nghĩa trong trong hàm. Ví dụ, mình click chuột phải vào một ô và chọn _Drill Down_ để lấy ra giá trị bên trong ô đó.

{{< figure src="./parameters5.png" width=60% >}}

Bây giờ, ta có thể thay thế tên của query vào trong hàm `Table.FirstN` như sau:

```
= Table.FirstN(Source, Keep_n_rows)
```

## 2. Custom Funtion

Giả sử chúng ta có 3 file dữ liệu như sau [(download files)](./data/Monthly-Sales-Data.zip):

{{< figure src="./custom-function.png" width=90% >}}

Đây là dữ liệu bán hàng theo từng tháng, dĩ nhiên là bên trong các file có các bảng có cấu trúc giống nhau nhưng sẽ khác nhau về mặt giá trị _(tên cột giống nhau)_.

Bây giờ chúng ta muốn viết một hàm với input là tên của file dữ liệu và output là một bảng dữ liệu đã được xử lý. Khi đó, thay vì phải xử lý từng file dữ liệu, chúng ta chỉ cần áp dụng hàm này với file dữ liệu mà ta muốn xử lý là xong.

{{< figure src="./custom-function2.png" width=80% >}}

Có hai cách để tạo một function trong Power Query:

- Cách thứ nhất: Chỉnh sửa _M Code_
- Cách thứ hai: Sử dụng tính năng _Create Function_

Trong ví dụ này, chúng ta sẽ sử dụng cách thứ nhất đó là chỉnh sửa M Code. Còn cách thứ hai, mình sẽ viết ở phần tiếp theo với một ví dụ khác. Cú pháp M Code để tạo một hàm:

```
(Variable as Data Type, Variable as Data Type) as Data Type =>

(Output Expression)
```

Trước khi đi tạo một hàm, chúng ta cần import một tập liệu để làm mẫu và thực hiện các thao tác biến đổi để có được một tập dữ liệu tốt:

{{< figure src="./custom-function3.png" width=90% >}}

Tiếp theo, ta sẽ tạo ra một _Query duplicate_ của query trên và đổi tên nó thành tên function mà bạn muốn tạo, ví dụ mình lấy tên là `ManualFunc`, sau đó bật _Advanced Editor_ lên để chỉnh sửa M Code của `ManualFunc`:

{{< image src="./custom-function4.png" width=100% >}}

Như các bạn thấy, chúng ta cần tạo một hàm, với input là một tham số thay thế cho đường link dẫn đến tên file mà mình đã bôi đậm trong hình _(click vào hình để nhìn rõ hơn)_. Bây giờ, ta sẽ sửa lại đoạn M code như sau và click vào _Done_ để hoàn tất:

{{< image src="./custom-function5.png" width=100% >}}

Giải thích:

- **filebinary:** là tên tham số hoặc tên biến mà chúng ta định nghĩa.
- **binary**: là kiểu dữ liệu của tham số.
- **table**: là kiểu dữ liệu mà functions sẽ trả về. Trong ví dụ này, output của chúng ta là một bảng.

Kết quả:

{{< figure src="./custom-function6.png" width=50% >}}

Bây giờ, ta sẽ áp dụng hàm này cho từng file. Đầu tiên ta cần import folder chứa cả 3 files dữ liệu:

{{< figure src="./custom-function7.png" width=70% >}}

Tiếp theo, ta vào _Add Column -> Invoke Custom Function_ để tạo cột dữ liệu mới sử dụng hàm `ManualFunc`

{{< figure src="./custom-function8.png" width=70% >}}

## 3. Create Function

### 3.1. Đặt vấn đề

Giả sử chúng ta có một file dữ liệu [Dirty Data.xlsx](./data/Dirty%20Data.xlsx) với 3 bảng dữ liệu như sau.

{{< figure src="./dirty-data-1.png" caption="2017 - 01" >}}

{{< figure src="./dirty-data-2.png" caption="2017 - 02" >}}

{{< figure src="./dirty-data-3.png" caption="2017 - 03" >}}

Không khó để nhận ra, phần dữ liệu mà chúng ta muốn lấy ra từ trong cả 3 bảng đều có cấu trúc giống nhau, nhưng trong mỗi bảng nó lại nằm ở những vị trí _(phạm vi)_ khác nhau. Mục tiêu của chúng ta là phải lấy ra được phần dữ liệu đó trong cả ba bảng sau đó tổng hợp lại thành một bảng duy nhất.

**Phương pháp**: Viết một hàm, với input là tên của các sheets trong file dữ liệu trên và output là một bảng dữ liệu đã được xử lý. Sau đó, áp dụng hàm trên cho từng sheets và sử dụng tính năng _Combine/Append_ để tổng hợp dữ liệu.

{{< figure src="./dirty-data-sheet.png" width=80% >}}

Trong phần trước, ta đã biết cách để tạo một function bằng cách chỉnh sửa M Code, cho nên phần này mình sẽ giới thiệu thêm một phương pháp nữa để tạo một function, đó là sử dụng _Create Function_. Với phương pháp này, Power Query sẽ tự động sửa M Code giúp chúng ta, khi chúng ta thực hiện các bước xử lý dữ liệu.

Tạo một hàm bằng _Create Function_ gồm 4 bước:

- **Bước 1:** Xác định đầu vào input của hàm, và tạo các tham số đại diện cho input này.
- **Bước 2:** Lấy ra một tập dữ liệu để làm dữ liệu mẫu. Tập dữ liệu này phải tham chiếu đến tham số đã tạo ở bước 1.
- **Bước 3:** Click chuột phải vào tập dữ liệu mẫu _(query)_, chọn _Create Function_ và đặt tên cho function của chúng ta.
- **Bước 4:** Quay trở tập dữ liệu mẫu ở bước 2, thực hiện các thao tác xử lý, biến đổi để có được một tập dữ liệu chuẩn. Khi mà chúng ta thực hiện các thao tác này, Power Query sẽ tự động thêm M Code vào functions mà chúng ta đã tạo ở bước 3.

Lý thuyết như vậy là đủ rồi, chúng ta bắt tay vào thực hành thôi!

Đầu tiên, ta sẽ import một bảng dữ liệu bất kỳ:

{{< figure src="./import-dirty-data.png" width=75% >}}

Sau đó, xóa các bước steps đi, chỉ để lại mỗi bước _Source_ và đổi tên query thành `Final Data`, dĩ nhiên bạn có thể đổi thành bất kỳ tên gì cũng được, mình để tên này vì cuối cùng mình sẽ áp dụng hàm tạo được trong query này.

{{< figure src="./final-data.png" >}}

### 3.2. Tạo parameters

Như đã nói trên, input của chúng ta là tên các sheets bên trong file dữ liệu. Ta sẽ tạo một tham số đại diện cho tên sheets. Mình đặt tên cho nó là `Sheet_Name`, tham số này có kiểu dữ liệu là Text.

Từ Tab Home trên thanh Ribbon, chọn _Manage Parameters -> New Parameters_:

{{< figure src="./sheet-name-parameters.png" width=60% >}}

{{< figure src="./sheet-name-parameters2.png" width=70% >}}

### 3.3. Tạo sample data

Click chuột phải vào _Final Data_ và chọn _Duplicate_ để tạo query mới, sau đó đổi tên query thành Sample Data:

{{< figure src="./duplicate.png" width=70% >}}

{{< figure src="./sample-data.png" >}}

{{< admonition type=notes title="Tắt type detection" open=false >}}
Trước khi đi tiếp, có lẽ mình phải tắt tùy chọn tự động xác định kiểu dữ liệu và tự động đặt tên headers cho các cột để tránh các sai lầm không cần thiết.

Ta vào File -> _Options and settings -> Query options_, ở phần Data Load của Global, tắt tùy chọn tự động xác định kiểu dữ liệu:

{{< figure src="./options.png" width=50% >}}

{{< figure src="./options2.png" width=75% >}}

{{< /admonition >}}

Click vào một Table bất kỳ để lấy ra file dữ liệu mẫu, ở đây mình lựa chọn Table của Sheet `2017-01`:

{{< figure src="./sample-data2.png" >}}

Một đoạn M Code đã được tạo ra như thế này:

```
= Source{[Item="2017-01",Kind="Sheet"]}[Data]
```

Và công việc của chúng ta đơn giản là thay cái tham số `Sheet_Name` mà chúng ta đã tạo vào tên sheets trong đoạn code trên: `Item="2017-01"` sửa thành `Item = Sheet_Name`:

```
= Source{[Item=Sheet_Name,Kind="Sheet"]}[Data]
```

{{< figure src="./sample-data3.png" >}}

Vậy là, ta đã có một tham `Sample Data` tham chiếu đến tham số `Sheet_Name` rồi.

### 3.4. Tạo function

Bước này, khá là đơn giản, chúng ta click chuột phải vào `Sample Data` và chọn _Create Function_, tiếp theo ta phải đặt tên cho function này. Mình đặt tên cho nó là `Transform_Data`:

{{< figure src="./Create-functions.png" width=60% >}}

{{< figure src="./Create-functions2.png" width=60% >}}

Cho đến bây giờ, chúng ta đã hoàn thành xong ba bước đầu tiên và được kết quả như sau:

{{< figure src="./Create-functions3.png" width=75% >}}

Tiếp theo, chúng ta không cần phải quan đến parameters hay là functions nữa, Power Query sẽ tự động xử lý giúp chúng ta. Việc còn lại của chúng ta là, quay trở lại xử lý tập dữ liệu `Sample Data` để có được một bảng dữ liệu chuẩn. Điểm bắt đầu của chúng ta ở đây:

{{< image src="./sample-data-first.png" width=100% >}}

### 3.5. Xử lý sample data

Đầu tiên, ta click vào _fx_ ở thanh _formula bar_, để thêm một step mới và đổi tên nó thành `Base_Table`

{{< figure src="./base-table.png" >}}

_Xác định và xóa các dòng null đầu tiên trong bảng dữ liệu_

**Step 1**: _Add Column -> Index Column_, đổi tên query thành `Row_idx`

**Step 2**: Xác định số lượng dòng đầu tiên bị null với công thức sau và đổi tên query thành `Find_null_rows`

```
= Table.FindText(Row_idx, "Region")
```

**Step 3**: Xóa các dòng null trong `Base_Table` bằng công thức sau và đổi tên query này thành `Remove_null_rows`:

```
= Table.Skip(Base_Table, Find_null_rows[Index]{0})
```

_Xác định và xóa các cột null đầu tiên trong bảng dữ liệu_

**Step 4**: Biến đổi `Remove_null_rows` bằng _Transpose_ và đổi tên query thành `Base_Table_2`

**Step 5**: Xử lý tương tự các bước từ `Step 1` đến `Step 3`

```
    Col_idx = Table.AddIndexColumn(Base_Table_2, "Index", 0, 1, Int64.Type),
    Find_null_cols = Table.FindText(Col_idx, "Region"),
    Remove_null_cols = Table.Skip(Base_Table_2, Find_null_cols[Index]{0})
```

**Step 6**: Biến đổi `Remove_null_cols` trở lại định dạng ban đầu bằng _Transpose_.

{{< figure src="./base-table2.png" >}}

_Cuối cùng, xử lý nốt các lỗi còn lại:_

- Removed Blank Rows
- Use Firse Row as Headers
- Unpivot

{{< figure src="./sample-data-output.png" >}}

### 3.6. Áp dụng functions

Quay trở lại với _Final Data_, ta sẽ áp dụng hàm `Transform_Data` với từng sheet của file dữ liệu bằng cách vào _Add Column -> Invoke Custom Function_:

{{< figure src="./invoke-functions.png" width=75% >}}

Tiếp theo, ta xóa tất cả các cột dữ liệu không cần thiết, chỉ để lại một cột duy nhất:

{{< figure src="./final-data2.png" >}}

Cuối cùng, click vào icon trong cột `Final_Data` và chọn _Expand_ để tổng hợp các bảng dữ liệu lại với nhau:

{{< figure src="./expand-column.png" width=40% >}}

{{< figure src="./final-data3.png" >}}
