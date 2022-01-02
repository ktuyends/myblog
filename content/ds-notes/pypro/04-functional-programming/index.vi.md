---
title: "Pypro - Lập trình hàm"
subtitle: ""
slug: functional-programming
date: 2021-12-24
lastmod: 2021-12-24
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
series: [Python Programming]
series_weight: 4
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
## 1. Functions

### 1.1. Định nghĩa hàm

Cú pháp:

```python
# Định nghĩa
def function_name(<parameters>):
    # statement(s)

# Gọi hàm
function_name(<arguments>)
```

### 1.2. Truyền đối số (arguments) 

Trường hợp 1: Truyền đối số dựa vào vị trí tương đối của tham số

```python
# Định nghĩa hàm
def f(qty, item, price):
    def f(qty, item, price):

# Truyền đối số
f(6, 'bananas', 1.74)
```

Trường hợp 2: Truyền đối số dựa vào tên tham số

```python
# Định nghĩa hàm
def f(qty, item, price):
    def f(qty, item, price):

# Truyền đối số
f(qty=6, item='bananas', price=1.74)

# Kết hợp, các tham số ở phía sau cùng
f(6, price=1.74, item='bananas')

# Hoặc
f(6, 'bananas', price=1.74)
```

Trường hợp 3: Giá trị mặc định của tham số

```python
# Định nghĩa
def f(qty=6, item='bananas', price=1.74):
    print(f'{qty} {item} cost ${price:.2f}')

# Khi gọi hàm, nếu k truyền đối số sẽ sử dụng giá trị mặc định
f(4, 'apples')
```

Trường hợp 4: Giá trị mặc định của tham số có dạng Mutable

Trong Python, giá trị mặc định của tham số chỉ được xác định lần đầu khi chúng ta gọi hàm. Nếu chúng ta gọi lại hàm mà không gán lại giá trị, nó sẽ sử dụng giá trị trước đó. Ví dụ: 



```python
# Định nghĩa hàm
def f(my_list=[]):
    print(id(my_list))
    my_list.append('###')
    return my_list

# Gọi hàm
f()
```

    2395892703424
    




    ['###']




```python
# Gọi hàm lần 2
f()
```

    2395892703424
    




    ['###', '###']



Trường hợp 5: Truyền đối số là đối tượng mutable (list, dict, set)

Trong trường hợp này, hàm có thể thay đổi các phần tử của đối tượng. Ví dụ




```python
# Định nghĩa hàm
def f(x):
    x[0] = "Monday"

# Tạo list
my_list = ['foo', 'bar', 'baz', 'qux']

# Gọi hàm
f(my_list)

# Xem kết quả
my_list
```




    ['Monday', 'bar', 'baz', 'qux']



### 1.3. Trả về kết quả với return

Lệnh return sẽ trả lại kết quả và sau đó kết thúc hàm. Chúng ta có thể sử dụng `return` để trả về một hoặc nhiều giá trị. Với nhiều giá trị ta sử dụng list, tuple,...Khi không trả về giá trị nào, hàm sẽ trả về `None`.

```python
def func_name(parameters):
    # Do something
    return value1, value2
```

### 1.4. Tham số `*args` và `**kwargs`

Chúng ta sử dụng `*args` trong trường hợp không xác định được số lượng đối số truyền vào trong hàm, ví dụ như các hàm tính `sum()`.

`*args` là một Tuple. Nếu các bạn muốn truyền một tuple vào hàm, ta cần thêm `*` vào trước tuple đó.

Ví dụ:

```python
# packing
def avg(*args):
    return sum(args) / len(args)

avg(1, 2, 3)
```

```python
# unpacking
def f(x, y, z):
    print(f'x = {x}')
    print(f'y = {y}')
    print(f'z = {z}')

t = ('foo', 'bar', 'baz')
f(*t)
```

Tương tự như `*args` sử dụng cho tuple thì `**kwargs` được sử dụng cho dictionary. Minh họa:

{{< figure src="arg1.png" >}}

{{< figure src="arg2.png" >}}

{{< figure src="arg3.png" >}}

### 1.5. Vị trí các tham số khi định nghĩa hàm

**Đối số theo vị trí và theo keyword**

{{< figure src="arg4.png" >}}

**Vị trí:**

{{< figure src="arg5.png" >}}

### 1.6. Docstrings

Mô tả về hàm:

```python
def func_name(parameters):
    """Descriptions

    Args:

    Return:

    """
    # Body

# Xem thông tin
print(func_name.__doc__)
help(func_name)
```


## 2. Lập trình hàm


### 2.1. Hàm ẩn danh lambda

Cú pháp:

```python
# hàm ẩn danh
var_name = lambda parameters: expression

# Gọi hàm nếu nó được gán
var_name(parameters)

# Gọi hàm nếu k được gán
(lambda parameters: expression)(parameters)
```

### 2.2. Map, Filter và Reduce

**Hàm *map()***

```python
# iter1, iter2 là các đối số của function
# function sẽ lặp qua từng giá trị 
map(function, iterable1, iterable2 ,...)
```

**Hàm *filter()***

Hàm này, ý nghĩa như cái tên. Nó hoạt động tương tự như hàm `map()` nhưng nó chỉ trả về các giá trị mà function trả về TRUE.

**Hàm *reduce()***

Hàm này, hoạt động tương tự các hàm trên, điểm khác là nó mang tính tích lũy.

```python
from functools import reduce
reduce(function, iterable)
```
