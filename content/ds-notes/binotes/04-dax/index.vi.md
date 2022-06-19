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

Trong bài trước, chúng ta đã tìm hiểu xong các khái niệm về _Data Models_ và các thành phần cơ bản của một data model. Trong bài này, đầu tiên chúng ta sẽ thực hành xây dựng một data model đơn giản. Sau đó, chúng ta sẽ học về DAX _(Data Analysis eXpressions)_, các bạn có thể hình dung DAX đơn giản chỉ là một tập của các hàm, toán tử và hằng số được sử dụng trong các công thức hoặc biểu thức tính toán để tạo ra các thông tin mới từ những dữ liệu có sẵn trong data model.

## 1. Làm quen với Power BI

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
