---
title: "Day 5 - Business statistics"
subtitle: ""
slug: 05-business-statistics
date: 2022-06-14
lastmod: 2022-06-14
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["BI"]
categories: []
series: [BI Course Notes]
series_weight: 5
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

Về cơ bản, bộ môn thống kê được chia làm hai nội dung chính: Thống kê mô tả _(Descriptive statistics)_ và thống kê suy diễn _(Inferential statistics)_. Trong đó:

- Thống kê mô tả sử dụng các bảng, đồ thị hoặc một số chỉ số thống kê để mô tả về dữ liệu thu thập được.
- Thống kê suy diễn thì được chia làm hai phần, thứ nhất là ước lượng tham số ví dụ như ước lượng về trung bình, độ biến động...Loại còn lại là kiểm định giả thuyết, dùng để đánh giá xem các tham số ước lượng được ở loại thứ nhất có chính xác hay không.

## 1. Descriptive Statistics

Trong phần này, chúng ta sẽ đi lướt nhanh qua một số chỉ số mô tả thường hay sử dụng.

### 1.1. Central of Tendency

{{< figure src="./01-descriptive-statistics/location_Parameter.png" width=70% >}}

Các chỉ số đo lường xu hướng tập trung:

**Mean**: Giá trị trung bình của một dãy số.

{{< figure src="./01-descriptive-statistics/mean_value.png" width=45% >}}

Ví dụ, số cốc trà sữa một học sinh uống trong một tuần, một nhóm gồm 5 học sinh, kết quả hỏi được như sau: _{21, 25, 10, 8, 11}_. Như vậy trung bình một học sinh một tuần uống 15 cốc.

{{< figure src="./01-descriptive-statistics/mean_value2.png" width=50% >}}

**Median**: là giá trị trung tâm của một dãy số được sắp xếp theo thứ tự các giá trị từ nhỏ nhất đến lớn nhất. Ví dụ dãy số _B = {8, 5, 7, 2, 1}_ sau khi được sắp xếp lại thành _B = {1, 2, 5, 7, 8}_ thì có giá trị `5` là giá trị chính giữa.

{{< figure src="./01-descriptive-statistics/median_odd_and_even_number.png" width=70% >}}

**Mode**: là giá trị có tỷ lệ xuất hiện nhiều nhất trong dãy số. Ví dụ _C = {1, 3, 3, 3, 5, 6, 7}_ thì số `3` là giá trị xuất hiện nhiều nhất.

{{< figure src="./01-descriptive-statistics/modal_en.png" width=60% >}}

Nhớ lại một số thang đo thống kê mình đã viết trong bài [đầu tiên](/01-bi-terminology/) của series:

- Thang đo định danh _(nomial)_ chỉ có thể tính được mode.
- Thang đo thứ bậc _(ordinal)_ có thể tính được mode và median.
- Thang đo khoảng _(interval)_ và tỷ lệ _(ratio)_ có thể tính được cả ba chỉ số.

**Lưu ý:** Trung bình _(Mean)_ là chỉ số thường được sử dụng nhất để mô tả dữ liệu, tuy nhiên khi dữ liệu của chúng ta có phân phối lệch về một bên quá nhiều _(distribution shapes)_ hoặc có những giá trị outliers (quá lớn hoặc quá nhỏ) thì giá trị trung bình tính được sẽ có xu hướng thiên vị và không phản ánh chính xác giá trị trung tâm. Trong trường hợp này, giá trị trung vị _(Median)_ sẽ phản ánh chính xác hơn.

{{< figure src="./01-descriptive-statistics/Mean_VS_Median.png" width=65% >}}

Một lưu ý nữa là đôi khi dữ liệu của chúng ta sẽ có các giá trị mean, median và mode bằng nhau. Cho nên chúng ta không nên quá ỷ lại vào những chỉ số như thế này, mà cần phải quan sát thêm về độ biến động và phân phối của dữ liệu.

### 1.2. Dispersion Parameter

Tham số phân tán đo lường sự biến động, phân tán của các điểm dữ liệu xung quanh các giá trị trung tâm. Chúng ta thường sử dụng độ lệch chuẩn _(standard deviation)_ và phương sai _(variance)_ để đo lường sự biến động các biến.

**Độ lệch chuẩn**: Đo lường sự biến động của các giá trị so với giá trị trung bình.

{{< figure src="./01-descriptive-statistics/standard-deviation.png" width=60% >}}

Độ lệch chuẩn là trung bình khoảng cách của tất cả các điểm dữ liệu so với giá trị trung bình. Do đó, nếu các điểm dữ liệu phân tán càng rộng thì độ lệch chuẩn cũng càng lớn. Có hai cách để tính độ lệch chuẩn tùy thuộc vào kích thước mẫu. Nếu chúng ta có toàn bộ dữ liệu thì độ lệch chuẩn được tính theo công thức sau:

{{< figure src="./01-descriptive-statistics/std_equ_text_en.svg" >}}

Trong trường hợp chúng ta không có đủ dữ liệu của toàn bộ tổng thể, thì độ lệch chuẩn tính theo công thức độ lệch chuẩn mẫu:

{{< figure src="./01-descriptive-statistics/std_equ_n_minus1_new.svg" >}}

**Phương sai**: Là bình phương của độ lệch chuẩn.

{{< figure src="./01-descriptive-statistics/Variance-vs-Standard-deviation.png" width=35% >}}

**Khoảng biến thiên** _(Range)_: Là khoảng cách giữa giá trị lớn nhất và giá trị nhỏ nhất của một phân phối.

{{< figure src="./01-descriptive-statistics/range_en.png" width=55% >}}

**Phân vị** _(Quartile)_: Dữ liệu được sắp xếp theo thứ tự các giá trị từ nhỏ nhất đến lớn nhất, sau đó được chia làm 4 phần bằng nhau. Giá trị nằm ở các vị trí 1/4, 1/2 và 3/4 của dữ liệu được gọi là điểm phân vị thứ nhất, median và điểm phân vị thứ 3.

{{< figure src="./01-descriptive-statistics/Quartile.png" width=40% >}}

**Khoảng tứ phân vị** _(Inter Quartile Range)_: là khoảng cách giữa điểm phân vị thứ ba và điểm phân vị thứ nhất. IQR thường được sử dụng để xác định các giá trị Outliers.

{{< figure src="./01-descriptive-statistics/Interquartile-Range.png" width=80% >}}

### 1.3. Normal Distribution

Khi nói về phân phối của dữ liệu, các bạn có thể hình dung đơn giản như thế này. Dữ liệu của chúng ta sẽ có giá trị lớn nhất và nhỏ nhất (áp dụng cho từng biến, cột trong tập dữ liệu), người ta chia cái khoảng giá trị này thành nhiều khoảng và trong mỗi khoảng này, đếm số lần xuất hiện của các giá trị. Sau đó dựa vào những kết quả thu được để tạo bảng phân phối và biểu đồ phân phối lịch sử _(Histograms)_.

{{< figure src="./01-descriptive-statistics/histograms.jpg" >}}

Tùy vào dữ liệu mà bạn làm việc, có thể bạn sẽ gặp nhiều kiểu phân phối khác nhau, tuy nhiên chúng ta sẽ thường sử dụng phân phối chuẩn _(Normal Distribution)_ hoặc có xu hướng biến đổi về phân phối chuẩn. Phân phối chuẩn là phân phối mà có ba giá trị mean, median và mode bằng nhau.

{{< figure src="./01-descriptive-statistics/normal-distrubution-large.svg" width=70% >}}

Nếu một phân phối chuẩn có trung bình bằng 0 và độ lệch chuẩn là 1 thì phân phối này được gọi là phân phối chuẩn hóa _(Standard Normal Distribution)_.

{{< figure src="./01-descriptive-statistics/Sec03.-StdNorm3-1024x279.png" width=80% >}}

### 1.4. Skewness và Kurtosis

**Hệ số bất cân xứng** _(Skewness)_: Dùng để đánh giá về mức độ cân xứng hoặc bất cân xứng (lệch) của một phân phối, các điểm dữ liệu có bị nghiêng về một phía hay không.

- Skewness < 0: Lệch trái _(Negative)_, phần đuôi bị lệch về bên trái.
- Skewness > 0: Lệch phải _(Positive)_ , phần đuôi bị lệch về bên phải

{{< figure src="./01-descriptive-statistics/skewness.png" width=80% >}}

**Hệ số nhọn** _(Kurtosis)_: Dùng để mô tả về độ nhọn của phân phối. Nếu một phân phối càng nhọn thì các điểm dữ liệu có xác suất càng tập trung về điểm trung tâm hơn.

{{< figure src="./01-descriptive-statistics/kurtosis.png" width=75% >}}

### 1.5. Correlation

Hệ số tương quan _(Correlation)_ được sử dụng để mô tả về mối quan hệ giữa hai biến. Hệ số tương quan càng cao thì hai biến càng có quan hệ chặt chẽ với nhau. Lưu ý, hệ số tương quan không phải quan hệ nhân quả. Nghĩa là không phải vì A xảy ra nên B xảy ra, mà nó chỉ đơn giản mô tả là A và B cùng xảy ra. Có thể là giữa A và B tồn tại một mối quan hệ nhân quả bắc cầu nào đó, cũng có thể là một mối quan hệ khác.

{{< figure src="./01-descriptive-statistics/correlation_coefficient.png" >}}

{{< admonition type=notes title="Excel Functions" open=true >}}

Một số hàm Excel thường sử dụng cho thống kê mô tả:

- Trung bình: AVERAGE
- Trung vị: MEDIAN
- Mode: MODE
- Độ lệch chuẩn: STDEV.S _(sample)_
- Hệ số biến thiên: STDEV.S/AVERAGE
- Khoảng biến thiên: MAX - MIN
- Phân vị: QUARTILE.EXC
- Skewness: SKEW
- Covariance: COVARIANCE.S
- Hệ số tương quan: CORREL
- Tần số: FREQUENCY

{{< /admonition >}}

## 2. Inferential Statistics

### 2.1. Population và Sample

Tổng thể _(Population)_ có thể hiểu đơn giản là tập hợp của tất cả các đối tượng nghiên cứu mà chúng ta quan tâm đến. Nhưng trên thực tế chúng ta không thể nào thu thập được tất cả các dữ liệu liên quan đến tổng thể, mà chỉ thu thập được một phần trong đó thôi. Thì cái phần thu thập được này, được gọi là mẫu _(Sample)_ của tổng thể. Và mục đích của thống kê suy diễn là dựa vào dữ liệu mẫu để suy diễn về tổng thể.

Để có thể thực hiện suy diễn thống kê thì dữ liệu mẫu phải đảm bảo hai đặc tính: dữ liệu phải được thu thập một cách ngẫu nhiên và dữ liệu phải đại diện được cho tổng thể.

### 2.2. Sampling Distributions

Việc lấy mẫu lặp đi lặp lại có cùng kích thước từ một tổng thể đưa đến một khái niệm về phân phối mẫu _(Sampling Distribution)_ của một tham số. Giả sử với mỗi lần lấy mẫu, chúng ta sẽ tính toán ra được một giá trị tương ứng của một tham số. Và chúng ta có thể hiểu phân phối mẫu của một tham số là phân phối của các giá trị tính được này.

{{< figure src="./02-inferential-statistics/sample-distribution.gif" >}}

### 2.3. Central Limit Theorem

Định lý giới hạn trung tâm cho rằng với cỡ mẫu đủ lớn từ một tổng thể và có độ biến động hữu hạn thì giá trị trung bình của tất cả các mẫu sẽ xấp xỉ bằng với trung bình của tổng thể. Và khi số lần lấy mẫu đủ lớn, người ta cho rằng phân phối mẫu _(sampling distribution)_ sẽ hội tụ về phân phối chuẩn.

{{< figure src="./02-inferential-statistics/Central-Limit-Theorem.webp" width=70% >}}

## 3. Misrepresenting Data
