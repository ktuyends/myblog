---
title: "Pypro - Làm quen với Python"
subtitle: ""
slug: intro-to-python
date: 2022-03-01
lastmod: 2022-03-01
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
series: [Python Programming]
series_weight: 3
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
## 1. Biến trong Python

Trong Python, mọi thứ đều là đối tượng, và một biến chỉ đơn giản là một tên, mang ý nghĩa tượng trưng, trỏ đến một đối tượng trong bộ nhớ. 

Ví dụ:

```python
# Phép gán
my_var = 100

# xem địa chỉ trong bộ nhớ của my_var
id(my_var)

# Xem kiểu dữ liệu của biến
type(my_var)
```

**Phép gán:**

```python
# Gán một giá trị cho một biến
my_var = 10

# Gán một giá trị cho nhiều biến
a = b = c = 10

# Gán nhiều giá trị cho nhiều biến
a, b = (5, 10)
a, b = 5, 10

# Lưu ý với string
a, b, c, d, e, f = 'Python'
a # 'P'

# đổi giá trị giữa 2 biến
x = 5
y = 10
x, y = y, x
```

{{< admonition type=notes title="Một số lưu ý về tên biến" open=true >}}
- Tên biến trong Python chỉ bao gồm các chữ cái, số và dấu gạch dưới `_`
- Tên biến phân biệt giữa các ký tự in hoa và in thường
- Tên biến không được trùng với các từ khóa trong Python
- Tên biến không được bắt đầu bằng số
{{< /admonition >}}


## 2. Kiểu dữ liệu

Trong Python, ta có 3 kiểu dữ liệu cơ bản:

- Kiểu dữ liệu số
- Kiểu dữ liệu Boolean
- Kiểu None

### 2.1. Kiểu dữ liệu số

Trong Python, các số phổ biến nhất là số nguyên *(int)* và số vô tỉ *(float)*. Ngoài ra còn một số kiểu khác như: Decimal *(số thập phân)*, Fraction *(số hữu tỉ - phân số)*, Complex *(Số phức)*.

**Số Nguyên:**

```python
# Số nguyên: -4, -2, 0, 4, 10
a = 10

# Kiểu - int
type(a)
```

**Số Thực - Float**

Số thực là các số mà trong đó có phần thập phân. Trong Python, sử dụng nguyên tắc xấp xỉ vì vậy các số float không phải là số chính xác mà chỉ là số xấp xỉ.

```python
# Số thực
my_float = 0.123

# Kiểu
type(my_float)
```

```python
# Làm tròn số thực: round, math.floor, math.ceil, math.trunc
my_float = 7.125
round(my_float, 2)

# Định dạng số thực
format(my_float, '.2f')
```

Lưu ý: Vì số thực trong Python là số xấp xỉ, khi so sánh hai số với nhau kết quả nhận được có thể không bằng nhau. Ví dụ:

```python
# Lưu ý khi so sánh hai số thực
0.1 + 0.2 == 0.3 # False

# Cách so sánh hai số thực
import math
math.isclose(0.1 + 0.2, 0.3) # True
```

**Số Decimal**

Số Decimal cũng là kiểu số thực, nhưng nó lưu trữ giá trị chính xác thay vì giá trị xấp xỉ như kiểu float.

```python
# Import
from decimal import Decimal

# Ví dụ
tax_rate = Decimal('7.25')/Decimal(100)
purchase_amount = Decimal('2.95')
tax_rate * purchase_amount # Decimal('0.213875')
```

**Phân Số - Fraction**

```python
# Cú pháp: Fraction(tử số, mẫu số)
from fractions import Fraction
Fraction(10, 4)
```

Chúng ta có thể chuyển đổi từ Decimal và Fraction về Float bằng hàm `float(gia_tri)`.

**Số Phức**

```python
# Cú pháp: a + bj
my_complex = 10 + 5j

# Phần thực, ảo
my_complex.real
my_complex.imag
```

### 2.2. Kiểu dữ liệu Boolean

Kiểu Boolean là kiểu mà chỉ có 2 giá trị: `True` hoặc `False`, tương ứng với `1` hoặc `0`.

```python
# my_bool
my_bool = True

# So sánh, TRUE
my_bool == 1
```

### 2.3. Kiểu dữ liệu None

None là một đối tượng đặc biệt trong Python mà ta có thể hiểu là không có gì, nó giống như một tập hợp rỗng trong toán học.

```python
# NoneType
my_var = None
```

### 2.4. Các toán tử làm việc với số

- Các phép toán cơ bản: *+ (cộng), - (trừ), * (nhân), / (chia), \*\* (lũy thừa)*
- Phép chia lấy phần nguyên: *a // b*
- Phép chia lấy phần dư: *a % b*
- Toán tử so sánh: *>, >=, <, <=, ==, !=*

### 2.5. Một số hàm làm việc với số

```python
# import thư viện
import math

# math.trunc(x), phần nguyên của một số
# math.floor(x), số được làm tròn > x
# math.ceil(x), số được làm tròn < x
# math.fabs(x), giá trị tuyệt đối
# math.sqrt(x), căn bậc hai
```

## 3. Câu lệnh và cú pháp

### 3.1. Cấu trúc một file script

Khi làm việc với Python, chúng ta thường sẽ có hai chế độ. Chế độ thứ nhất là chế độ tương tác, ở các môi trường như *IPython, Jupyter Notebook*,...Chế độ thứ hai là chế độ *Script*.

Một file script - `my_script.py` có cấu trúc như sau:

```python
#!/usr/bin/env python3

# Dòng đầu tiên là shebang, khai báo phiên bản Python
# Dòng bên dưới là docstring, mô tả về file script

"""
Mô tả về file Script
"""

# Phần còn lại là nội dung chính của file
print("Hello World!")
```

### 3.2. Viết những dòng code dài

Một số quy tắc ngắt dòng:

```python
# Ngắt dòng
a = [1, 
    2, 
    3]

# Ngắt dòng và comment, ] không sử dụng sau comment
a = [1, #first element
    2, #second element
    3, #third element
    ]

# Ngắt dòng sử dụng ký tự `\`
if a > 5 \
    and b > 10 \
    and c > 20:
    print('yes!!')
```

```python
# Ngắt dòng sử dụng ()
import math
example_value = (63 / 25) * (
                (17 + 15 * math.sqrt(5))
               /(7 + 15 * math.sqrt(5))
                ) 
print(example_value)

# Ngắt dòng sử dụng ("a" "b") = "ab"
message_text = (f'Trời hôm nay '
                f'mưa rất to')
print(message_text)
