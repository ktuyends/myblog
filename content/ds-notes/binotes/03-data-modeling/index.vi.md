---
title: "Day 3 - Data modeling (basic)"
subtitle: ""
slug: 03-basic-data-modeling
date: 2022-05-26
lastmod: 2022-05-26
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["BI"]
categories: []
series: [BI Course Notes]
series_weight: 3
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

{{< figure src="./Report_Development_Process.png" >}}

## 1. Data Model

### 1.1. Khái niệm

Data Model trong Power BI hiểu đơn giản thì nó là một tập hợp của các bảng _(table)_ được liên kết với nhau theo một mối quan hệ (relationships) dựa trên các keys trong bảng. Chúng ta có thể hình dung mỗi một bảng sẽ thể hiện một vấn đề nào đó. Ví dụ các vấn đề như sales, products, customers...

Data model là một khung nền tảng bắt buộc phải có trước khi bắt tay vào phân tích dữ liệu. Tùy thuộc vào chất lượng của data model mà sẽ hưởng nhiều hay ít đến hiệu quả của các reports, visualizations và dashboards.

### 1.2. Các bước xây dựng data model

**Chuẩn bị dữ liệu:**

- Bước 1: Import và transform data
- Bước 2: Merge và append các table để giảm số lượng các bảng trong Data model.
- Bước 3: Đổi tên các bảng và columns để thân thiện hơn với người dùng.
- Bước 4: Xóa các columns không sử dụng đến.
- Bước 5: Chuyển đổi kiểu dữ liệu và các định dạng về dạng chuẩn.

**Tạo data model:**

- Bước 6: Xác định và tạo mối liên kết giữa các bảng.

**Bổ sung thêm thêm thông tin cho data model:**

- Bước 7: Tạo cấu trúc phân cấp (hierarchies)
- Bước 8: Tạo các bảng, cột và measures
- Bước 9: Ẩn các cột dữ liệu chỉ mang ý nghĩa liên kết giữa các bảng hoặc làm trung gian cho các tính toán mà không có nhiều ý nghĩa về mặt phân tích. ví dụ như các cột `id`.

## 2. Data model components

### 2.1. Fact and dim tables

Giả sử trong database có 100 bảng dữ liệu, thì ta không thể nào hoặc nếu có thể thì cũng không nên tạo một cái data model với 100 bảng, liệu một data model như vậy nó có hợp lý hay không. Chúng ta nên cố gắng xây dựng một cái data model đơn giản, sắp xếp dễ hiểu với ít bảng nhưng vẫn phải đảm bảo đủ các thông tin cần thiết. Vậy dựa vào đâu để xác định bảng nào là bảng nên đưa vào data model và bảng nào thì không?

Đầu tiên, chúng ta cần đi xác định **dữ liệu transactions**. Đây là những dữ liệu có tính chất thay đổi thường xuyên theo thời gian, ví dụ như thay đổi theo ngày, theo giờ, theo tuần,...thì với những dữ liệu này, người ta chỉ lưu trữ những thông tin định danh cơ bản ví dụ như id của một đối tượng,...và các con số mang tính chất tính toán liên quan đến đối tượng được định danh đó.

Với dữ liệu transactions người ta sẽ không lưu trữ các thông tin chi tiết về một đối tượng. Vậy khi muốn biết các thông tin chi tiết đó ta phải tìm ở đâu? Thì thông thường ta sẽ phải lấy thông tin ở các bảng dữ liệu khác để bổ sung thêm thông tin cho bảng transactions.

Người ta phân loại các bảng dữ liệu mà bổ sung thông tin cho bảng transactions thành 4 nhóm:

- **Who:** Các thông tin liên quan đến con người, ví dụ các sản phẩm được bán cho ai...
- **What:** Các thông tin liên quan đến sự vật, ví dụ như các sản phẩm được bán là sản phẩm nào...
- **When:** Thông tin về thời gian, ví dự như sản phẩm được bán ở thời điểm nào, tháng nào, quý nào...
- **Where:** Thông tin về địa lý, ví dụ như sản phẩm này được bán ở địa chỉ nào, khu vực nào...

Các bảng transactions còn được gọi là **Data table** hoặc **Fact table**.

Các bảng bổ sung thông tin cho _bảng Fact_ được gọi là bảng **Dimensions**, bảng **Dim** hoặc **Lookup table**.

{{< figure src="./data-table.png" width=70% >}}

Với mỗi bảng Dim, ta sẽ có một cột khóa chính. Đây là cột chứa các giá trị duy nhất dùng để phân biệt các đối tượng. Bảng Fact sẽ chứa nhiều cột khóa ngoại, được sử dụng để xác định các mối liên kết _(relationships)_ với bảng Dim.

Thông thường, trong nhiều bộ phận hoặc phòng ban, chúng ta sẽ gặp phải tình huống đó là tất cả dữ liệu được lưu trữ trong một bảng duy nhất, bảng này được gọi là _flat table_ hoặc _single table_. Tuy nhiên, cách lưu trữ dữ liệu thế này không phải là cách tối ưu, bởi vì dữ liệu trong một số cột sẽ bị lặp đi lặp lại rất là nhiều lần hoặc đôi khi thông tin giữa các cột cũng bị trùng lặp với nhau. Ví dụ:

{{< figure src="./single-table.png" width=75% >}}

Do đó, chúng ta phải tách _single table_ thành các bảng nhỏ hơn như _data table_ và _lookup table_ để hạn chế việc lặp dữ liệu và giúp cho việc lưu trữ được tối ưu hơn.

### 2.2. Schema

Sau khi chúng ta đã xác định và phân loại được hai loại bảng là _data table_ và _lookup table_, việc tiếp theo chúng ta phải làm đó là sắp xếp lại các bảng sao cho nó hợp lý và dễ hiểu. Và cái việc sắp xếp các bảng như thế này người ta gọi là **schema**.

Có nhiều loại schema, nhưng mà trong Power BI chúng ta sẽ thường làm việc với **star schema**.

{{< figure src="./star-schema-example2.png" width=65% >}}

{{< figure src="./star-schema.jpg" width=65% >}}

Ngoài ra, chúng ta còn có **snowflake schema**, đây là loại data model biến thể của _star schema_ mà sẽ có thêm các bảng để bổ sung thông tin cho bảng Dim _(lookup table)_.

{{< figure src="./snowflake.png" width=75% >}}

{{< figure src="./snowflake2.png" width=75% >}}

Thực tế, khi xây dựng data model, ta sẽ có nhiều bảng Fact cùng chia sẻ với nhau một hoặc một số bảng Dim:

{{< figure src="./galaxy.png" width=75% >}}

### 2.3. Relationships

Relationships hiểu đơn giản là mối liên kết giữa một table với một table khác được xác định bởi một single column từ mỗi table, bạn không thể định nghĩa một mối quan hệ dựa vào nhiều column nhưng bạn có thể tạo một column mới kết hợp các column trên với nhau để sử dụng làm cột xác định mối liên kết.

### 2.4. Cardinality

{{< figure src="./cardinality.webp" width=70% >}}

Cardinality, là một thuộc tính của relationships và trong Power BI thì có ba loại cardinality chính:

- One-to-one
- One-to-many
- Many-to-many _(Many-to-one + one-to-many)_

### 2.5. Cross filter direction

{{< figure src="./cross-filter-direction.png" width=70% >}}

Relationships trong data models đôi khi người ta còn hiểu nó là một bộ lọc _(filter)_ từ bảng này qua bảng khác thì trong Power BI, bộ lọc _filter_ được chia làm hai loại:

- Bộ lọc một chiều _(single direction)_: Với trường hợp này, chúng ta chỉ có thể lấy dữ liệu từ bảng khác theo chiều của mũi tên mà không thể làm ngược lại được. Với mối quan hệ _one-to-many_ luôn luôn là một chiều từ _one -> many_.
- Bộ lọc hai chiều _(both)_: Ngược lại với một chiều, chúng ta có thể lọc dữ liệu được ở cả hai chiều.

### 2.6. Hierarchies

Hierarchies, là những dữ liệu có tính chất phân cấp. Ví dụ như thời gian thì có thể phân cấp như: _năm > quý > tháng > tuần > ngày_.

## 3. Làm quen với Power BI

Power BI không chỉ là một công cụ làm báo cáo mà mọi người vẫn hay sử dụng để xây dựng các reports đẹp mắt. Nó còn là một nền tảng cung cấp một loạt các tính năng từ chuẩn bị dữ liệu _(data preparing)_ đến mô hình hóa dữ liệu _(data modeling)_ và trực quan hóa dữ liệu _(data visualizations)_.

{{< figure src="./data-process.jpg" width=80% >}}

Đây cũng là một trong những hệ sinh thái phân tích dữ liệu được xây dựng rất tốt, mang lại cho người dùng khả năng đóng góp vào quy trình phân tích dữ liệu của tổ chức theo nhiều cách. Từ chia sẻ bộ dữ liệu _(datasets)_, làm các reports và tạo các dashboards đến sử dụng các thiết bị di động để thêm một số nhận xét vào reports, đặt các câu hỏi và gửi chúng đến cho những người dùng có liên quan.

Tất cả những điều này chỉ mang lại kết quả phân tích tốt khi chúng ta thực hiện các bước chính xác trong việc xây dựng hệ sinh thái Power BI. Một báo cáo đẹp không có ý nghĩa gì nếu nó hiển thị số liệu kinh doanh không chính xác hoặc nếu báo cáo quá chậm để hiển thị sẽ ảnh hưởng đến những người có nhu cầu sử dụng nó.

Một trong những khía cạnh quan trọng nhất của việc xây dựng hệ sinh thái Power BI là có một bộ dữ liệu tốt. Trong các tình huống thực tế, bạn thường phải lấy được dữ liệu từ các nguồn khác nhau và import nó vào Power BI. Sau đó, bạn cần đưa ra một data model được thiết kế tốt để đảm bảo nó luôn đại diện cho các dữ liệu hỗ trợ cho các mục đích phân tích, xây dựng reports, dashboards và cuối cùng là storytelling.

{{< figure src="./power-bi-layer.jpg" >}}

Trong Power BI, chúng ta có ba giao diện chính. Thứ nhất là **Power Query layer**, trong layer này, bạn sẽ lấy dữ liệu từ các nguồn khác nhau, biến đổi và làm sạch dữ liệu đó và load nó vào Data Model.

{{< figure src="./power-query-layer.jpg" >}}

**Data Model layer** gồm _data view_ và _model view_. Sau khi chúng ta hoàn thành việc chuẩn bị dữ liệu trong Power Query layer, chúng ta sẽ tải dữ liệu vào Data Model layer. Với chế độ _Data View_, chúng ta có thể thấy dữ liệu cơ bản của mình sau khi nó đã được biến đổi. Và tùy thuộc vào chế độ kết nối, dữ liệu có thể được hiển thị hoặc không.

{{< figure src="./data-view.jpg" caption="_Data view; storage mode: Import_" >}}

{{< figure src="./data-view2.jpg" caption="_Data view; storage mode: DirectQuery_" >}}

Như tên gọi của nó, trong _Model View_ chúng ta có một tập hợp các bảng và các liên kết giữa chúng.

{{< figure src="./model-view.jpg" caption="_Model view_" >}}

Điểm đến cuối cùng trong quy trình phân tích dữ liệu của chúng ta là **Data Visualization layer** _(Report view)_, đây là nơi chúng ta có thể thỏa sức sáng tạo với các biểu đồ và phân tích của mình.

{{< figure src="./report-view.jpg" >}}
