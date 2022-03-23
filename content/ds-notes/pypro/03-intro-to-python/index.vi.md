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
```

### 3.3. Comments

Có hai cách viết comments trong Python:

```python
# Cách 1:
# This is a single-line comment.

# Cách 2:

"""This is a
multiline string that
also works as a multiline comment. """
```

Khi viết comments trong Python, ta chú ý một số nguyên tắc sau:

- Comments theo sau code, nên viết cách code 2 khoảng trắng.
- Comments thường là các câu hoàn chỉnh, trường hợp comments quá dài ta có thể viết trên nhiều dòng.  
- Chúng ta phân tách các comments bằng một comment trống.
- Các comments nên có cùng mức độ thụt lề dòng với khối code định ghi chú.

Ví dụ:

```python
# Here is a comment about this code:
someCode()

# Here is a lengthier block comment that spans multiple lines using
# several single-line comments in a row.
#
# These are known as block comments.

if someCondition:
    # Here is a comment about some other code:
    someOtherCode()  # Here is an inline comment.
```
{{< admonition type=notes title="Docstrings" open=true >}}
Trong Python, Docstrings là các comments nhiều dòng, có thể xuất hiện ở đầu của một module, hoặc theo sau các câu lệnh `def` và `class` khi khởi tạo các hàm hoặc các lớp. Chúng cung cấp thông tin về module, class, function hoặc các phương thức được định nghĩa.

Một số công cụ tạo tài liệu tự động, sẽ sử dụng các thông tin này để xây dựng các files help, hoặc web pages.
{{< /admonition >}}


## 4. Cấu trúc điều khiển

### 4.1. Các toán tử Boolean

- Toán tử so sánh: *==, !=, >, >=, <, <=*
- So sánh về mặt đối tượng: *is, is not*
- Toán tử boolean: *and, or, not, and not, or not*
- Toán tử: *in, not in*

### 4.2. Một số lưu ý

{{< admonition type=notes title="Lưu ý 1:" open=true >}}
Khi so sánh hai iterable cùng loại, Python sẽ lấy lần lượt từng phần tử trong iterable ra để so sánh:

```python
'Kteam' == "Kteam" # True
'Free' == 'Education' # False
```
{{< /admonition >}}

{{< admonition type=notes title="Toán tử == và toán tử is" open=true >}}
Toán tử `==` được sử dụng để so sánh hai đối tượng về mặt giá trị. Toán tử `is` được sử dụng để so sánh xem hai đối tượng có cùng vị trí trong bộ nhớ hay không.

Với các tập hợp các phần tử có thứ tự xác định, toán tử `==` sẽ so sánh các phần tử tương ứng với từng vị trí cụ thế. Ngược lại với các tập hợp mà các phần tử không có thứ tự xác định, nó sẽ dựa vào giá trị bên trong.

```python
# Ví dụ 1
a = [10, 20, 30]
b = [10, 20, 30]
a is b # False
a == b # True

# Ví dụ 2:
a = (10, 20, 30)
b = (20, 10, 30)
a == b # False

# Ví dụ 3
a = {10, 20, 30}
b = {30, 20, 10}
print(a is b, a == b) # False, True

# Ví dụ 4
a = {'a': 1, 200: 'two hundred'}
b = {200: 'two hundred', 'a': 1}
print(a is b, a == b) # False, True
```
{{< /admonition >}}

{{< admonition type=notes title="Đối tượng singleton" open=true >}}
Theo mặc định các số nguyên từ -5 đến 256 (đối tượng singleton) được Python tạo sẵn, vì vậy nó có địa chỉ xác định. Nên khi ta sử dụng toán tử `is` để so sánh hoặc sử dụng `id(num)` để kiểm tra vị trí thì nó luôn cố định.

Một số đối tượng singleton khác như: *True, False, None*. Với những đối tượng này, ta nên sử dụng toán tử `is` thay vì sử dụng `==`.
{{< /admonition >}}

{{< admonition type=notes title="Kiểu boolean" open=true >}}
Khi nhắc đến kiểu dữ liệu boolean, mọi thứ biểu thị giá trị `0`, rỗng, `None`,...sẽ được hiểu là False. Ngược lại là True.

```python
bool(0), bool(-1), bool(1), bool(100) # (False, True, True, True)
bool(None) # False
```
{{< /admonition >}}

### 4.3. Câu lệnh if

```python
# Câu lệnh đơn giản
if <dieu_kien>:
    # Nếu điều kiện trả về True
    # Thực thi câu lệnh

# If...else
if <dieu_kien>:
    # Nếu điều kiện trả về True
    # Thực thi câu lệnh
else:
    # Nếu điều kiện trả về False
    # Thự thi câu lệnh
```

```python
# if...elif...else
if <dieu_kien_1>:
    # Nếu điều kiện 1 trả về True
    # Thực thi câu lệnh
elif <dieu_kien_2>:
    # Nếu điều kiện 2 trả về True
    # Thực thi câu lệnh
else:
    # Nếu các điều kiện trả về False
    # Thự thi câu lệnh

# if rút gọn
<value_if_True> if <dieu_kien> else <value_if_False>
```

{{< admonition type=notes title="Cấu trúc Match - Case" open=true >}}
Đây là một cấu trúc mới xuất hiện trong Python 3.10. Thay vì kiểm tra các điều kiện như câu lệnh `if`, nó kiểm tra các trường hợp có thể xảy ra. Cú pháp:

```python
my_var = 10
match my_var:
    case value_1:
        # Do something
    case value_2:
        # Do something
    case _:
        # Thực hiện nếu tất cả các lệnh trên bị bỏ qua
```

{{< /admonition >}}

### 4.4. Vòng lặp for

```python
# Cú pháp
# iterable: string, list, tuple, dictionary, set, range()
# iterable: Là một đối tượng, có khả năng trả về lần lượt từng giá trị 
for var in iterable:
    # Thực thi các câu lệnh

else: # Có thể có hoặc không
    # Nếu vòng lặp không bị break
    # Thì thực thi else sau khi kết thúc vòng lặp 
```

### 4.5. Vòng lặp while

```python
# Cú pháp
while <dieu_kien>:
    # Thực thi cho đến khi điều kiện trả về False

else: # Có thể có hoặc không
    # Nếu vòng lặp không bị break
    # Thì thực thi else sau khi kết thúc vòng lặp 
```

### 4.6. break, continue và pass

- break: thoát khỏi vòng lặp
- continue: thoát khỏi lượt lặp hiện tại, chuyển sang lượt lặp tiếp theo
- pass: Không thực thi gì hết, chỉ mang ý nghĩa giữ chỗ

> Nếu sử dụng câu lệnh `try-finally` bên trong vòng lặp, thì `finally` luôn luôn thực thi, dù cho vòng lặp gặp phải break hoặc continue.

### 4.7. enumerate và zip

```python
# zip()
a = ['a', 'b', 'c']
b = [5, 10, 15]
zip(a, b) # [('a', 5), ('b', 10), ('c', 15)]

# enumerate
my_list = ['monday', 'tuesday', 'sunday']
enumerate(my_list) # [(0, 'monday'), (1, 'tuesday'), (2, 'sunday')]
```

### 4.8. Assertion

```python
assert <expression>
```

Khi gặp câu lệnh `assert`, Python sẽ đánh giá biểu thức logic đi kèm. Nếu biểu thức trả về `True` thì câu lệnh sẽ kết thúc và không có gì xảy ra, ngược lại nếu biểu thức trả về `False` thì một ngoại lệ _(exception)_ sẽ được trả về.

