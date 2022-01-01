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
## 1. Lướt qua Python

### 1.1. Chú thích

Chú thích trên một dòng

```python
# Đây là chú thích trên một dòng
```

Chú thích trên nhiều dòng

```python
"""
Đây là chú thích
Trên nhiều dòng
Khác nhau
"""
```

### 1.2. Phép Gán

Cách 1: Gán một giá trị cho một biến

```python
ages = [12, 16, 19]
```

Cách 2: Gán một giá trị cho nhiều biến

```python
a = b = 10
```

Cách 3: Gán nhiều giá trị cho nhiều biến

```python
m, n = 17, 6
```

### 1.3. Các toán tử cơ bản

**Phép toán số học**

- Phép cộng: *a + b*
- Phép trừ: *a - b*
- Phép nhân: *a \* b*
- Phép chia: *a / b*
- Phép chia lấy phần nguyên: *a // b*
- Phép chia lấy phần dư: *a % b*
- Lũy thừa: *a ** b* 

**Phép so sánh**

- Lớn hơn: *a > b*
- Lớn hơn hoặc bằng: *a >= b*
- Nhỏ hơn: *a < b*
- Nhỏ hơn hoặc bắng: *a <= b*
- Bằng: *a == b*
- Khác: *a != b*

**Phép toán logic**

- *A and B*
- *A or B*
- *not A*, *not(A)*

**Toán tử in, not in**

```python
a = [5, 10, 15]
5 in a
10 not in a
```

**Toán tử is, is not**

```python
# Trả về True nếu cùng một đối tượng
x = [1, 2, 3]
y = [1, 2, 3]
print(x is y)
```

### 1.4. Print

Trường hợp 1: Hàm `print()` được sử dụng để hiển thị kết quả của một đối tượng, hoặc một biểu thức

```python
# Một đối tượng
print(""This is a sample string"")

# Một biểu thức
print(10 + 15)

# Print nhiều tham đối tượng, các giá trị cách nhau bởi dấu cách
print(5, 10, 15)
```

Trường hợp 2: Nối các string

```python
# Sử dụng dấu + để kết nối các string
print("Last year's revenue was " + "3" + " million euros")
```

Trường hợp 3: Định dạng bằng f-strings

```python
# Chèn giá trị của các biến, biểu thức vào string sử dụng {}
# Ví dụ:
revenue = 3
print(f"Last year's revenue was {revenue} million euros")

# Có thể chèn cả revenue
print(f"Last year's revenue was {revenue = } million euros")
```

Trường hợp 4: Newline



```python
# Sử dụng \n để ngắt string
print("See how I broke\nthis line?")
```

    See how I broke
    this line?
    

Theo mặc định, câu lệnh `print()` sẽ chèn một newline sau khi được thực thi. Để tránh điều này ta có thể sử dụng tham số `end`:

```python
print("First string", end=' ')
print("Second string")
```

## 2. Cấu trúc rẽ nhánh

**Trường hợp 1**

{{< figure src="if1.png" >}}

Cú pháp:

```python
if <dieu_kien>:
    # Do something
```

**Trường hợp 2**

{{< figure src="if2.png" >}}

Cú pháp:

```python
if <dieu_kien>:
    # Do something
else:
    # Do something
```

**Trường hợp 3**

{{< figure src="if3.png" >}}

Cú pháp:

```python
if <dieu_kien>:
    # Do something
elif <dieu_kien>:
    # Do something
...
else:
    # Do something
```

**Trường hợp 4:**

{{< figure src="if4.png" >}}

Cú pháp:

```python
<do something> if <condition TRUE> else <do something>
```


## 3. Vòng lặp

### 3.1. Vòng lặp while

Vòng lặp while thực thi câu lệnh cho đến khi `<dieu_kien>` trả về giá trị *False*.

{{< figure src="while.png" >}}

Cú pháp 1:

```python
while <dieu_kien>:
    # Do something
```

Cú pháp 2: Else trong vòng lặp for, thực thi sau khi vòng lặp kết thúc nếu không gặp break

```python
while <dieu_kien>:
    # Do something
else:
    # Do something
```

### 3.2. break, continue và pass

Trong Python, có một số lệnh giúp chúng ta thay đổi luồng xử lý của vòng lặp như:

- break: Thoát khỏi vòng lặp hiện tại
- continue: Bỏ qua phần còn lại của lần lặp hiện tại, bước vào lần lặp tiếp theo
- pass: Không thực thi nhiệm vụ nào, nó được sử dụng như một cách để giữ chỗ

### 3.3. Vòng lặp for

{{< figure src="for.png" >}}

Cú pháp 1:

```python
for var in iterable:
    # Do something

else: # Có thể có hoặc không
    # Do something
```

Cú pháp 2:

```python
for var in range(start = 0, stop, step = 1):
    # Do something
```

### 3.4. Zip và Enumerate

Trong Python:

- *zip(list1, list2)*: Trả về một cặp tuple kết hợp các phần tử của nhiều lists
- *enumerate()*: Trả về một cặp tuple có dạng *(index, value)*



## 4. Functions

### 4.1. Tạo hàm

{{< figure src="func.png" >}}

Cú pháp:

```python
def func_name(arguments):
    # Do something
    return value
```

Phân biệt argument (đối số) và parameter (tham số):

- Parameter: Được gọi khi định nghĩa hàm, nó đại diện cho một giá trị mà hàm sẽ nhận được khi được gọi
- Argument: Đại diện cho giá trị truyền cho tham số khi thực hiện gọi hàm

### 4.2. Hàm ẩn danh lambda

Cú pháp:

```python
# hàm ẩn danh
var_name = lambda parameters: expression

# Gọi hàm nếu nó được gán
var_name(parameters)

# Gọi hàm nếu k được gán
(lambda parameters: expression)(parameters)
```

### 4.3. Map, Filter và Reduce

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

## 5. Một số cấu trúc dữ liệu cơ bản

### 5.1. List

**Tạo một list:**

```python
# List rỗng
a = []
b = list()

# List chứa item
c = [it1, it2,...,itn]

# Xem độ dài của list
len(c)
```

**Truy cập các phần tử của list:**

```python
# Vị trí (idx) của các phần tử trong list bắt đầu từ 0 -> len(list) - 1
list_name[idx]
```

**Xóa phần tử khỏi list dựa vào vị trí**

Trường hợp 1: Sử dụng `del`



```python
# Tạo list
brands = ["Fender", "Gibson", "Ibanez"]

# Copy
brands_2 = brands

# Xóa sử dụng del
del brands[1]

# Xem kết quả 
print(f"{brands = }")
print(f"{brands_2 = }")
```

    brands = ['Fender', 'Ibanez']
    brands_2 = ['Fender', 'Ibanez']
    

> Lưu ý: như ta thấy, trong trường hợp trên chúng ta chỉ đơn giản là gán 2 tên biến đến cùng một list, chứ không phải là tạo ra hai list.

Trường hợp 2: Sử dụng phương thức `pop`

```python
# Xóa ở vị trí idx
list_name.pop(idx)

# Xóa vị trí cuối
list_name.pop()
```

Trường hợp 3: Xóa tất cả các phần tử

```python
# Sử dụng clear
list_name.clear()
````

**Tạo bản sao của list**

```python
# Phương thức copy
var_name = list_name.copy()
```

**Xem vị trí của một phần tử**

```python
# index
list_name.index("item_value")
```

**Xóa phần tử dựa vào giá trị**

```python
# sử dụng remove
list_name.remove("item_value")
```

**Thay đổi giá trị trong list**

```python
# sử dụng idx
list_name[idx] = new_value
```

**Sub-lists**

{{< figure src="slicing.png" >}}

{{< figure src="slicing2.png" >}}

```python
#slicing, trả về các phần tử từ start đến end-1
list_name[start=0 : end=len(the_list)] : step=1]

# Ví dụ
c[1:3]
```

**Thêm phần tử vào list**

- Thêm item vào cuối list: *list_name.append(item)*
- Thêm item vào một vị trí nào đó trong list: *list_name.insert(idx, item)*
- Thêm các phần tử từ một list khác: *list_name.extend("other_list")*

**Giải nén list:**




```python
# Ví dụ
models = [
    "Stratocaster",
    "Telecaster",
    "Les Paul",
    "Flying V",
    "RG"
    ]

# Unpacking, * đại diện cho các giá trị còn lại
first_model, *remaining_models = models

# Xem kết quả
print(f"{first_model = }")
print(f"{remaining_models = }")
```

    first_model = 'Stratocaster'
    remaining_models = ['Telecaster', 'Les Paul', 'Flying V', 'RG']
    

**Sắp xếp các phần tử trong list**

```python
# Đảo ngược vị trí - reverse()
list_name.reverse()

# sort
list_name.sort(reverse = False)

```

### 5.2. Tuples

Tuples tương tự như list ngoại trừ:

- Tuple sử dụng `()` thay vì `[]`
- Chúng ta không thể thay đổi các giá trị trong Tuple

Một số ví dụ với tuple:

```python
# Tạo tuple có 1 phần tử
tp1 = (item, )

# Gán
a, b = 10, 5
a, b = (9, 0.3)
(a, b) = ("a", "b")

# Chuyển đổi giữa tuple và list sử dụng:
list(t)
tuple(l)
```



### 5.3. List Comprehension

Trường hợp 1: Cơ bản

{{< figure src="list-com1.png" >}}

Trường hợp 2: Kết hợp với điều kiện `if`

{{< figure src="list-com2.png" >}}

Trường hợp 3: Lồng nhau

{{< figure src="list-com3.png" >}}


### 5.4. Set

{{< figure src="set.png" >}}

Set trong Python ta có thể hiểu nó như một tập các giá trị có đặc điểm sau:

- Các giá trị là duy nhất, không được lặp lại
- Các giá trị trong Set không có thứ tự, không thể truy cập dựa vào index
- Set là mutable (có thể thay đổi), nên ta có thể thêm các phần tử vào Set
- Các giá trị trong Set có thể có nhiều kiểu dữ liệu khác nhau
- Set là mutable, nhưng các giá trị trong Set phải là immutable


**Tạo Set:**

```python
# Sử dụng {item1, item2,....}
S = {'red', 'green', 'blue'}

# Sử dụng hàm tạo
S2 = set([1, 2, 3])
```

**Thêm phần tử vào Set:**

```python
# Thêm một phần tử
S.add(item)

# Thêm nhiều phần tử
S.update(list_item)
```

**Xóa phần tử:**

```python
# Sử dụng remove
S.remove(item)

# Sử dụng discard
S.discard(item)

# discard giống remove, chỉ khác là nếu có error, discard trả về nothing

# Sử dụng pop, xóa item ngẫu nhiên và trả về item bị xóa
S.pop()

# Xóa tất cả
S.clear()
```

**Phép toán tập hợp**

```python
# Phép hợp: union hoặc |
A | B
A.union(B)

# Phép giao: Intersect, &
A.union(B)
A.union(B)

# Phép trừ: difference, -
A - B
A.difference(B)

# Symmetric Difference, symmetric_difference, ^
A ^ B
A.symmetric_difference(B)
```

**Frozenset**

Frozenset trong Python, tương tự như Set nhưng điểm khác biệt là nó có kiểu immutable, vì vậy chúng ta không thể thực hiện các thao tác thêm, xóa hay sửa đổi. Tuy nhiên Frozenset vẫn thực hiện được các phép toán tập hợp.

```python
# Hàm frozenset
F = frozenset(iterable)
```





### 5.5. Dictionary

{{< figure src="dict.png" >}}

Dictionary trong Python, ta có thể hiểu đơn giản là một tập hợp các cặp `key:value`.

- Các keys là duy nhất, không được lặp lại, nó có thể hiểu giống index trong list
- Các keys là immutable

**Tạo Dictionary**

```python
# Sử dụng {}
D = {'name': 'Bob',
     'age': 25,
     'job': 'Dev',
     'city': 'New York',
     'email': 'bob@web.com'}

# Sử dụng hàm dict()
D = dict(name = 'Bob',
         age = 25,
         job = 'Dev')
```

```python
# Dict from list
L = [('name', 'Bob'),
     ('age', 25),
     ('job', 'Dev')]

D = dict(L)

# Dict from tuple
T = (['name', 'Bob'],
     ['age', 25],
     ['job', 'Dev'])

D = dict(T)

# Dict from keys
keys = ['a', 'b', 'c']
defaultValue = 0

D = dict.fromkeys(keys,defaultValue)
```

**Truy cập các giá trị trong Dict**

```python
# Sử dụng key
# Nếu không có key sẽ trả về lỗi
dict_name["key"]

# Sử dụng phương thức get()
# Nếu không có key sẽ không trả về gì hết
dict_name.get("key")
```

**Thêm hoặc sửa phần tử**

```python
# Sử dụng key
dict_name["new_key"] = value
```

**Gộp hai dict với nhau**

```python
# sử dụng phương thức update
D1.update(D2)
```

**Xóa các phần tử**

```python
# Sử dụng pop
D1.pop("key")

# Sử dụng del
del D1["key"]
```

**Xóa phần tử được thêm vào cuối cùng**

```python
# Sử dụng popitem
D.popitem()
```

**Xóa toàn bộ phần tử**

```python
# Sử dụng clear
D.clear()
```

**Xem danh sách keys, values**

```python
# key
list(D.keys())

# Value
list(D.values())

# all
list(D.items())
```

**Vòng lặp với Dict**

```python
D = {'name': 'Bob',
     'age': 25,
     'job': 'Dev'}

for x in D:
    print(D[x])
# Prints Bob 25 Dev
```

**Sử dụng phép trừ với key**

```python
D = {0: 'A', 1: 'B', 2: 'C', 3: 'D', 4: 'E', 5: 'F'}
removeKeys = [0, 2, 5]
D.keys() - removeKeys
```

## 6. Tính toán trong Python

### 6.1. Python modules

**Import và sử dụng modules**

```python
# import module math
import math

# Sử dụng, ví dụ tính số e
math.e

# Tính giai thừa
math.factorial(10)
```

```python
# import sử dụng tên định danh
import math as maths
maths.cos(maths.pi)
```

```python
# import trực tiếp hàm vào không gian tên
from math import factorial as fac
fac(3)
```

### 6.2. Numbers

Một số loại số trong Python

- Số nguyên (int)
- Số thực (float)
- inf (dương vô cùng)
- nan (not a number)

Một số hàm làm việc với số nguyên:

- *math.factorial(n)*: Giai thừa, tính hoán vị
- *math.perm(n, k)*: Chỉnh hợp, lấy k phần tử từ n phần tử và sắp xếp theo một thứ tự
- *math.comb(n, k)*: Tổ hợp, lấy k phần tử từ n phần tử
- *round(n, digit)*, *math.ceil()*, *math.floor()*, *math.trunc()*: Làm tròn số
- *math.e*: số e
- *math.exp(n)*: $e^n$
- *math.pow(a, n)*: $a^n$
- *math.sqrt(n)*: $\sqrt{n}$
- *math.log(a, base = e), math.log2(a), math.log10(a)*

### 6.3. Số phức

**Tạo số phức**

```python
# import cmath
import cmath

# Tạo số phức, a + bj
z = complex(a, b)

# Phần thực
z.real

# Phần ảo
z.imag

# Số phức liên hợp
z.conjugate()
```

### 6.4. Symbolic

```python
# Tạo
import sympy as sym

x = sym.Symbol('x')
p = x**3 - 2*x**2 - 5*x + 6

# Phân tích thừa số
sym.factor(p)

# Sub
p.subs(x, 3)

# Giới hạn, x -> 3
sym.limit(p, x, 3)

# Đạo hàm
sym.diff(p, x)

# Tích phân
sym.integrate(p, x)
```

### 6.5. Số ngẫu nhiên

**Tạo số ngẫu nhiên**

```python
# import
import random

# Tạo số nguyên ngẫu nhiên
random.randint(start, end)

# Số ngẫu nhiên giữa 0 và 1
random.random()
```

```python
# Đánh dấu kết quả với seed
random.seed(10)
[random.randint(1, 10) for i in range(6)]

# GỌi lại kết quả
random.seed(10)
[random.randint(1, 10) for i in range(6)]
```

**Chọn mẫu (sampling)**

```python
# Chọn nhiều mẫu
random.sample(list_name, n)

# Chọn một mẫu
random.choice(list_name)
```

## 7. Strings

### 7.1. Single, double, và triple quotes

**Trường hợp 1: Sử dụng `'...'`**

```python
# string
a = 'Hôm nay là cuối năm'
```

**Trường hợp 2: Sử dụng `"..."`**

```python
# tương tự như '...'
b = "Hôm nay là cuối năm"
```

**Trường hợp 3: String trên nhiều dòng**

```python
"""
Đây là một đoạn string
Được viết trên nhiều dòng
"""
````

**Trường hợp 4: Kết hợp `'` và `"`**

```python
"That is Franz's cat toy."
```

**Newline**

```python
# newline sử dụng \n
c = "But 'print' breaks\nthe line at the character."
print(c)

# Output
# But 'print' breaks
# the line at the character.
```

**Raw string**

```python
s = r"C:\src\code\chapter-01"
print(s)

# output: 'C:\\src\\code\\chapter-01'
```

### 7.2. Substrings

Sử dụng `in` và `not in` xem một substrings có nằm bên trong một chuỗi string hay không.

```python
# Python phân biệt ký tự in hoa và in thường

"Quantum" in "Quantum computing" # output: True
"QUANTUM" not in "Quantum computing" # output: False
``` 

Một số phương thức với string:

- *str.upper()*
- *str.lower()*
- *str.capitalize()*
- *str.casefold()*: Được dùng khi muốn so sánh string mà không cần quan tâm đến ký tự in hoa hay in thường

### 7.3. Truy cập các ký tự

Tương tự như với list, mỗi ký tự trong string tương ứng với một phần tử.

> Lưu ý: String là immutable, vì vậy ta không thể sửa đổi các ký tự bên trong một chuỗi

### 7.4. Tạo string

**Concate sử dụng `+`**

Chúng ta có thể sử dụng `+` để nối các chuỗi với nhau, ví dụ:

```python
"Hôm nay " + "trời nhiều mây"
```

**Định dạng chuỗi với f-strings**

```python
# 3 chữ số phần thập phân {number:format}
f"This is 1/7 to 3 decimal places: {(1/7):.3f}"
```

**Phương thức format**

```python
# vd1
greet_positional = 'Hello {}!'
greet_positional.format('Fabrizio')

# vd2
greet_positional_idx = 'This is {0}! {1} loves {0}!'
greet_positional_idx.format('Python', 'Heinrich')

# vd3
keyword = 'Hello, my name is {name} {last_name}'
keyword.format(name='Fabrizio', last_name='Romano')
```

**Phương thức join nối các phần tử của một list**

```python
# chr là ký tự phân cách giữa các phần tử
words = ['If', 'you', 'have', 'a', 'list']
print('chr'.join(words))
```

**Phương thức replace thay thể một substr**


```python
s = "My favorite guitar is a Fender."
s.replace("Fender", "Gibson")
# output: 'My favorite guitar is a Gibson.'
```

### 7.5. Một số phương thức khác

- *str.isalnum()*: Nếu str chỉ gồm các ký tự alphabetic hoặc chữ số
- *str.isalpha()*: Nếu str chỉ gồm các ký tự alphabetic
- *str.isdigit()*: Nếu str chỉ gồm các số từ 0 đến 9
- *str.islower()*: Nếu tất cả các ký tự in thường
- *str.isupper()*: Nếu tất cả các ký tự in hoa
- *str.isspace()*: Nếu tất cả các ký tự là khoảng trắng, newline hoặc `''`
- *str.startswith('chr')*: Nếu str bắt đầu bằng chr
- *str.endswith('chr')*: Nếu str kết thúc bằng chr
- *str.split('chr', n = all)*: Tách chuỗi thành list
- *str.rsplit('chr')*
- *str.strip()*: Loại bỏ khoảng trắng trước và sau str
- *str.lstrip(), str.rstrip()*


