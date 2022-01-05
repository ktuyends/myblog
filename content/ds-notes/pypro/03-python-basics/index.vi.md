---
title: "Pypro - Làm quen với Python"
subtitle: ""
slug: basic-python
date: 2021-12-23
lastmod: 2021-12-23
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
## 1. Hằng số

Hằng số, là các biến có giá trị cố định, không thể thay đổi. Ví dụ:

```python
# Số
4, 6, 1.4, 6.5

# Ký tự
'something', 'string'
```

## 2. Keywords

Là các từ được định nghĩa bởi Python, vì vậy ta không thể sử dụng chúng để đặt tên biến.

```python
# Một số keyword
if, else, for, while, is, as, or, not, and, None, def, class, return, yield, pass, raise
```

## 3. Biến

Trong Python, biến:

- Là một tên trỏ đến một đối tượng nào đó
- Phân biệt giữa ký tự in hoa và in thường
- Không cần khai báo khi sử dụng

**Một số kiểu đặt tên biến**

```python
# Kiểu 1
myVar, myString42, rawData

# Kiểu 2
MyVar, MyString30, FileData

# Kiểu 3
my_var, my_string12, some_data3
```

**Biến không có kiểu**

```python
# Đầu tiên my_var được gán bởi một số
# Sau đó nó được gán bởi một string, 34 sẽ được Python tự động xóa
my_var = 34
my_var = "I am string"
my_var = [1,2,3,4]
my_var = 4.0
```

**Biến chỉ là các tham chiếu**

```python
a = 34
b = a
a = 20
print(a, b) # 20, 34

# a trỏ đến 34
# b cũng trỏ đến 34 mà không phải a
# a thay đổi tham chiếu đến 20, không ảnh hưởng đến b
```

## 4. Các toán tử

- Toán tử số học: +, -, *, /, % (chia lấy phần dư), // (chia lấy phần nguyên), ** (lũy thừa)
- Toán tử so sánh: ==, !=, >, >=, <, <=
- Toán tử logic: and, or, not
- Toán tử khác: is, is not, in, not in
- Ngoài ra còn có toán tử gán, toán tử với bit

**Toán tử logic: and, or, not**

```python
# and: True and True = True, other False
a=20
b=30
if a > 10 and b < 50:
    print('printed')
if a > 42 and b < 50:
    print('not printed')

# or: False or False = False, other True
if a > 10 or b < 10:
  print('printed')
if a > 20 or b < 30:
  print('not printed')

# not True = False
a = 39
if not isinstance(a, int):
    print('not printed')
if not isinstance(a, str):
      print('printed')
````

**Toán tử is, is not**

```python
# is: Kiểm tra hai đối tượng xem có cùng kiểu hay không
my_var1 = 42
my_var2 = 42
my_var1 is my_var2 # True

# Python tự động tạo ra các giá trị trong khoảng (-5, 256), vì vậy nó có địa chỉ cố định
# Tương tự như ví dụ trên, ví dụ này trả về false
x = 500
y = 500
x is y # False

# Xem địa chỉ
print(id(x)) # 2868472346320
print(id(y)) # 2868472342896

# Nếu not đi với if, nên viết là if not, thay vì if is not
if not x is y:
    print('x và y không trỏ về cùng một địa chỉ')
```

**Toán tử in, not in**

```python
# in kiểm tra xem một giá trị có nằm trong một tập hợp hay không
my_list = [23,5,32,65,20]
print(20 in my_list) # True
print(30 in my_list) # False
print(10 not in my_list) # True
print(32 not in my_list) # False
```

## 5. Phép gán

```python
# Một giá trị cho một biến
my_var = 'Something'

# Gán một giá trị cho nhiều biến
a = b = c = 10

# Gán nhiều giá trị cho nhiều biến
a, b, c = 5, 10, 15

# Đổi giá trị
a, b = b, a
```

## 6. Khi câu lệnh quá dài

```python
# Sử dụng "\" tại cuối dòng để tiếp tục câu lệnh trên dòng khác
text = "This is text 1." \
"This is text 2" \
"And I can also continue here in the next line."

# Với phương thức, thuộc tính
output = something
         .some_fun()
         .calling_other_fun()
```

## 7. Chú thích

```python
# this is a single line comment
# TODO: this is a todo comment, useful in IDEs like Visual Studio Code/Pycharm

"""this is a
multiline comment
"""
```

## 8. Thụt lề

Trong Python, các khối mã được xác định dựa vào mức độ thụt lề. Thường mặc định là 4 khoảng trắng với một cấp độ. Thụt lề thường được sử dụng với các câu lệnh rẽ nhánh, vòng lặp, định nghĩa hàm, class, xử lý lỗi,...Ví dụ:

```python
# Không thụt lề sau if nên gặp lỗi IndentationError
if 10 > 5:
print('printed') # IndentationError

# Ví dụ 2:
if 10 > 5:
    # preferred indentation
    print('printed')

print('block code ends') # Khối mã mới
```

## 9. Namespace (Không gian tên)

Trong Python, có ba loại không gian tên:

- Loại 1 (built-in): Là các hàm được tích hợp sẵn trong Python
- Loại 2 (global): Do người dùng định nghĩa bên ngoài function/class
- Loại 3 (local): Do người dùng định nghĩa bên trong function/class

Ví dụ:

```python
# built-in namespace
print(), len(), map(), range(), list(), set(), str(), etc. 
```

```python
## global namespace
# importing any modules adds them global namespace
import time
# variables and functions
my_var = 10
def my_fun():
    pass
```

```python
## local namespace
def some_fun():
    # variables and functions defined here
    my_var = 10
    def my_fun():
        pass
```
