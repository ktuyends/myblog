---
title: "Pypro - Cấu trúc dữ liệu"
subtitle: ""
slug: python-data-structures
date: 2022-03-02
lastmod: 2022-03-02
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
## 1. Strings

### 1.1. Tạo strings

String trong Python là một chuỗi gồm nhiều ký tự nối lại với nhau. Để tạo một chuỗi, về cơ bản ta có 3 cách sau:

```python
# Tạo chuỗi sử dụng '...'
my_str = 'Hello'

# Tạo chuỗi sử dụng "..."
my_str = "Today, is a new day"

# Docstring, multi-line string
my_str = """Learn Python
         Programming"""

# Đếm số ký tự trong một string
len(my_str)
```

Trong một số dự án Python, có thể chúng ta sẽ gặp một số chuỗi mà đằng trước nó được thêm ký tự `r'` hoặc `R'`. Những chuỗi này được gọi là _raw string_.

_Raw string_ ta hiểu đơn giản là, các ký tự _escape_ sẽ không có ý nghĩa đặc biệt mà nó chỉ là các ký tự bình thường. Lưu ý, nếu sử dụng ký tự `\` ở cuối _raw string_ thì số lượng ký tự `\\` phải là số chẵn nếu không sẽ xảy ra lỗi.

### 1.2. Toán tử với string

- Toán tử `+`: Nối các chuỗi với nhau.
- Toán tử `*n`: Hiểu đơn giản nó là toán tử `+` thực hiện `n` lần.

**Phương thức Join**

```python
# Nối các phần tử trong một iterable
# Trong đó chr là ký tự nối
'chr'.join(iterable)
```

### 1.3. Slicing

Chúng ta có thể cắt một chuỗi trong Python thành các chuỗi nhỏ hơn (substring) sử dụng cú pháp:

```python
# Xác định ký tự ở vị trí idx
# Tính từ trái sang phải: 0, 1, 2, 3,...
# Tính từ phải sang trái: -1, -2, -3,...
my_str[idx]

# slicing 
# lấy các ký tự tính từ start đến end-1
# nếu có step thì mỗi ký tự cách nhau step lần
my_str[start:end]
```

### 1.4. Tách chuỗi với split

Cú pháp:

```python
# Sep, là ký tự xác định tách chuỗi, mặc định là khoảng trắng
# maxsplit là số lần tách, mặc định là vô hạn
str.split(sep, maxsplit)

# Phương thức splitlines tách dòng
# keepends: Mặc định là k giữ lại ký tự xuống dòng
str.splitlines(keepends)

# Phương thức partition tách chuỗi thành 3 phần: trước, ký tự tách, sau
str.partition(sep)
```

### 1.5. Tách số trong chuỗi

Với phần này, ta sử dụng _regular expression_, đầu tiên ta cần _import_ thư viện `re`:

```python
# import re module
import re
```

Pattern chúng ta sẽ sử dụng gồm có:

- `\d`: Đại diện cho các số.
- `\D`: Đại diện cho các ký tự không phải số.

**Sử dụng re.findall để tách các số**

```python
s1 = '1ab23cdef456'

# ['1', '2', '3', '4', '5', '6']
m1 = re.findall(r'\d', s1)  

# ['6', '2', '5', '6', '2', '0', '2', '1', '2', '1', '3', '0']
s2 = 'Thứ 6 ngày 25 tháng 6 năm 2021, 21:30'
m2 = re.findall(r'\d', s2)  
```

**Sử dụng re.findall để tách các dãy số**

```python
s = 'Thứ 6 ngày 25 tháng 6 năm 2021, 21:30'

# ['6', '25', '6', '2021', '21', '30']
m = re.findall(r'\d+', s) 
```

**Sử dụng re.sub để tìm kiếm và thay thế**

```python
s1 = '1ab23cdef456'
m1 = re.sub(r'\D','', s1) # 123456

s2 = 'Thứ 6 ngày 25 tháng 6 năm 2021, 21:30'
m2 = re.sub(r'\D','', s2)  # 625620212130
```

**Sử dụng re.search để tìm số, dãy số đầu tiên**

Lưu ý là `re.search` không trả về một chuỗi mà trả về một đối tượng `match`. Vì vậy, để xem kết quả ta phải sử dụng thêm các phương thức như `start(), end(), spane()`

```python
s1 = '1ab23cdef456'
m1 = re.search(r'\d', s1)
m1.group() # 1

s2 = 'Thứ 6 ngày 25 tháng 6 năm 2021, 21:30'
m2 = re.search(r'\d', s2)  
m2.group() # 6
```

```python
s = 'Năm 2021, thứ 6 ngày 13 21:30'
m = re.search(r'\d+', s)  
m.group() # 2021
m.start() # 4
m.end() # 8
m.span() # (4, 8)
```

### 1.6. Xóa các ký tự 

Phương thức `strip()` được sử dụng để xóa ký tự xuất hiện ở cả hai đầu của string và tạo ra một string mới. Cú pháp:

```python
# org_str là chuỗi số ban đầu
# chars là tập hợp các ký tự muốn xóa ở hai đầu
new_str = org_str.strip('chars')

# Ví dụ
org_str  =  "address1"
new_str1 = org_str.strip('as1')  # ddre
```

Phương thức `strip()` chỉ xóa được các ký tự ở hai đầu của string, nếu muốn xóa toàn bộ các ký tự chúng ta sử dụng `replace()`:

```python
str.replace("old_chr", "new_chr"))
```

### 1.7. Tìm kiếm và thay thế

Phương thức `find()`:

```python
# Nếu tìm thấy sẽ trả về index của chr đầu tiên tìm thấy
# Nếu không tìm thấy, trả về -1
# start, end chỉ định phạm vi tìm kiếm, mặc định là toàn bộ string
str.find('chr', [start, end])
```

Phương thức `index()` tương tự như `find()` nhưng nếu không tìm thấy sẽ trả về một lỗi.

Phương thức `replace()`:

```python
# count: chỉ định số lần thay thế, mặc định là all
str.replace('old_chr', 'new_chr', count)
```

### 1.8. Định dạng chuỗi

Để định dạng chuỗi, chúng ta sử dụng cú pháp _f-string_:

```python
# Tổng quát
# {value:pattern} là phần cần được định dạng
f'abc {value:pattern} xyz'
```

Cú pháp của Pattern: `{:align width type}`

- Tham số type: _s (string), n (số nguyên), d (số thập phân), e hoặc E (kiểu mũ), f (float), % (phần trăm)_.
- Tham số width: Độ dài tối thiểu.
- Tham số align: _< (căn trái), > (căn phải), ^ (căn giữa), n (thay thế chỗ trống bằng n)_.
- Pattern `{:,f}`: Thêm dấu `,` vào phần nguyên.
- Pattern `{:.nf}`: n chữ số phần thập phân.

### 1.9. Một số nội dung khác

- Phương thức `count('chr', [start, end])`: Đếm số lần xuất hiện của ký tự.
- Phương thức kiểm tra: _isalpha(), isalnum(), isdecimal(), isdigit(), isnumeric(), islower(), isupper(), istitle()_.
- Phương thức chuyển đổi: _upper(), lower(), title(), capitalize(), swapcase()_.

## 2. Tuples

{{< figure src="tuple.jpg" >}}

### 2.1. Tuples là gì?

Giả sử ta có một hàm `translate(text, target_language)`, trong đó `text` là strings mà bạn muốn dịch và `target_language` là ngôn ngữ mà bạn muốn dịch sang. Hàm này sẽ trả về hai giá trị:

- Một chuỗi mới được dịch nghĩa từ chuỗi `text`
- Độ tin cậy thể hiện chất lượng của kết quả dịch.

Thông thường hàm sẽ trả về một kết quả ở một thời điểm, nhưng bây giờ chúng ta lại muốn trả về hai kết quả. Khi đó, ta có thể sẽ dùng đến Tuples.

Tuples là một cấu trúc dữ liệu được tích hợp sẵn trong Python:

- Bạn có thể lưu trữ nhiều giá trị thuộc các kiểu dữ liệu khác nhau bên trong một Tuple.
- Các giá trị bên trong tuple là có thứ tự, nghĩa là mỗi phần tử có một vị trí index xác định.
- Tuples là immutable, có nghĩa là, bạn không thể thay đổi một tuple sau khi nó được tạo ra. Tuy nhiên trong trường tuple có chứa giá trị thuộc kiểu mutable ví dụ như list, thì ta có thể thay đổi các giá trị bên trong list đó.

### 2.2. Tạo Tuples

```python
# Tuple rỗng
empty_tuple = ()
empty_tuple = tuple()

# Tuple có một giá trị
my_tuple = (10, )
my_tuple = 10, 

# Tuple có nhiều giá trị
t1 = (1, 2, 3, 'Python')
t2 = 1, 2, 3, 'Python'
```

### 2.3. Các toán tử với Tuples

| Cú pháp | Ý nghĩa |
|--|---|
| `x in t `| Kiểm tra xem tuple `t` có chứa giá trị bên trong biến `x` hay không. |
| `t + s` | Tạo một tuple mới chứa các giá trị từ tuple `t` và `s` |
| `t*n` | Tạo một tuple mới, lặp lại tuple `t` n lần. |
| `t[i]` | Phần tử ở vị trí `i` |
| `t[i:j:k]` | slicing |
| `len(t)` | Trả về số phần tử của tuple `t` |
| `min(t)` | Phần tử có giá trị nhỏ nhất bên trong tuples. |
| `max(t)` | Phần tử có giá trị lớn nhất bên trong tuples. |
| `t.count(x)` | Đếm số lần xuất hiện `x` bên trong tuple `t` |

### 2.4. Unpacking một tuple

```python
# Giả sử ta có
my_tuple = (1, 2, 3, 4, 5)

# Một số cách unpacking
one, two, three, four, five = my_tuple # one = 1, two =2,...
one, *_, four, five = my_tuple
```

Ví dụ sử dụng unpacking:

```python
from math import sqrt
def distance(a, b):
    return sqrt(a**2 + b**2)

point2D = (5, 3)

# call function distance
# Push 1 tuple vào một hàm phải unpacking nó sử dụng dấu *
distance(*point2D)
```

### 2.5. NameTuples

Giả sử bạn có một tuple như sau: `dot = (1.5, 98, 75, 12, 12.5)`, bạn có biết mỗi phần tử trong tuple đại diện cho cái gì không nếu chỉ nhìn vào các con số? Dĩ nhiên là không thể rồi, vì vậy chúng ta phải sử dụng đến NameTuples.

Ví dụ:

```python
from collections import namedtuple

# Tuple Person, với 3 phần tử đại diện cho name, age, country
# Đối số đầu tiên là tên tuple
# Đối số thứ hai có thể là một string, tuple hoặc list
Person = namedtuple('Person', 'name age country')

# Tạo giá trị
bob = Person('Bob', 31, 'UK')

# Xem các giá trị
bob.name
bob.age
bob.country
```

Một số cách sửa đổi NameTuples:

```python
# Update các giá trị
# NameTuples cũng là immutable vì vậy phải gán lại
bob = bob._replace(age = 33, country = "US")

# Thêm thuộc tính vào NameTuples
new_fields = Person._fields + ('City', )
NewPerson = namedtuple('NewPerson', new_fields)
bob = NewPerson(*bob, 'Washington')
```

Như vậy, với NameTuples ta có thể tóm tắt như sau:

- Đầu tiên là phải tạo một đối tượng nametuple gồm tên `Tuple_Name` và các thuộc tính. Để lấy danh sách các thuộc tính sử dụng `Tuple_Name._fieds`
- Tiếp theo, tạo các thể hiện của đối tượng bằng `Tuple_Name()`, để update thuộc tính sử dụng `Tuple_Name._replace()`


## 3. Lists

List tương tự như Tuples, nhưng nó thuộc nhóm Mutable nên chúng ta có thể thực hiện các thao tác sửa đổi nó.

### 3.1. Tạo list

Một số cách tạo list:

| Cú pháp | Ý nghĩa |
|--|--|
| `[]` | List rỗng |
| `[x1, x2, x3, … ]` | Tạo list, với các phần tử `x1, x2, x3,...` |
| `[expr1, expr2, ... ]` | Tạo list, với các phần tử là kết quả từ `expr1, expr2,...`|
| `[expr for var in iter]` | List comprehension. |
| `list(iterable)` | Tạo list sử dụng hàm list. |

### 3.2. Slicing

Về cơ bản, bạn có thể nghĩ slicing với list tương tự như với strings.

### 3.3. Một số phương thức 

Thêm phần tử vào list:

| Cú pháp | Ý nghĩa |
|--|--|
|`lst.append(x)`| Thêm phần tử `x` vào list `lst`|
|`lst.extend(iter)`| Thêm tất cả các phần tử từ iterable vào list `lst`|
|`lst.insert(i, x)`| Chèn phần tử `x` tại vị trí `i` trong list `lst`|

Ví dụ:

```python
a = [1, 2, 3]
b = [4, 5, 6]

# 1. List concatenation operator +
l_1 = a + b

# 2. List append() method
l_2 = []

for el in a:
    l_2.append(el)
    
for el in b:
    l_2.append(el)

# 3. List extend() method
l_3 = []
l_3.extend(a)
l_3.extend(b)

# 4. Asterisk operator *
l_4 = [*a, *b]

# 5. List comprehension
l_5 = [el for lst in (a, b) for el in lst]
```

Xóa phần tử:

| Cú pháp | Ý nghĩa |
|--|--|
|`lst.clear()`| Xóa tất cả các phần tử, list `lst` trở thành list rỗng.|
|`lst.pop()`| Xóa phần tử dựa vào idx, trả về giá trị là phần tử bị xóa, mặc định là phần tử cuối cùng.|
|`lst.remove(x)`| Xóa phần tử đầu tiên có giá trị giống `x`|
| `del lst[]`| Xóa một hoặc nhiều phần tử.|

Sắp xếp:

| Cú pháp | Ý nghĩa |
|--|--|
|`lst.reverse()`| Đảo ngược vị trí của các phần tử trong list `lst`|
|`lst.sort()`| Sắp xếp các phần tử trong list theo giá trị tăng dần.|

Một số phương thức khác:

| Cú pháp | Ý nghĩa |
|--|--|
|`lst.count(x)`| Đếm số lần xuất hiện của phần tử `x` bên trong list.|
|`lst.index(x)`| Trả về vị trí đầu tiên xuất hiện `x` trong list.|
|`lst.copy()`| Tạo một bản copy của list `lst`| 

{{< admonition type=notes title="Shallow Copy và Deep Copy" open=true >}}

Lưu ý khi copy một đối tượng list. Chúng ta có hai khái niệm:

- Shallow Copy: Tạo ra một list mới, các phần tử trong list mới có cùng tham chiếu với các phần tử trong list cũ. 
- Deep Copy: Thay vì sao chép các tham chiếu, nó sao chép đối tượng. Deep copy không được tích hợp trong Python vì vậy ta phải sử dụng thư viện `copy` và hàm `copy.deepcopy(lst)`

{{< /admonition >}}

### 3.4. List comprehension

Một số dạng list comprehension:

```python
# Dạng 1: Đơn giản
[Expression for var in iterable]

# Dạng 2: Thêm if
[Expression for var in iterable if conditional]

# Dạng 3: Nested list comprehension
[Expression for var in iterable for var2 in iterable2]

# Dạng 4: List comprehension with if-else
[value1 if conditional else value2 for var in iterable]
```

## 4. Sets

Sets là cấu trúc dữ liệu, gồm nhiều phần tử trong đó:

- Các phần tử có giá trị thuộc kiểu immutable.
- Các phần tử trong Sets là duy nhất, không lặp lại.
- Các phần tử trong Sets không có thứ tự, nên ta không thể xác định giá trị dựa vào vị trí như các kiểu dữ liệu khác như list, string và tuples.

### 4.1. Tạo sets

```python
# Sets không chứa giá trị
empty_set = set()

# Tạo set bằng {}
s1 = {"Harry", "Ron", "Hermine"}

# Tạo set bằng hàm set(list)
s2 = set(["Harry", "Ron", "Hermine"])

# Thêm phần tử vào set
s3 = set()
s3.add("Harry")
s3.add("Ron")
s3.add("Hermine")
```

### 4.2. Một số phương thức

```python
Gryffindors = {"Harry", "Ron", "Hermine", "Neville",
               "Seamus", "Ginny", "Fred", "George"}

## Set Conversion
Weasleys = set(["Ron", "Ginny", "Fred"])
# {'Ron', 'Fred', 'Ginny'}

## Add Element
Weasleys.add("George")
# {'Ron', 'Fred', 'Ginny', 'George'}

## Remove Element
# Remove trả về lỗi nếu giá trị k tồn tại
# Tương tự như Remove, có discard(), nếu k tồn tại discard trả về None
Gryffindors.remove("Neville")
# {'Ron', 'Hermine', 'George', 'Harry', 'Ginny', 'Seamus', 'Fred'}

## Membership
'Ginny' in Gryffindors
# True

## Size
len(Weasleys)
# 4
```

```python
## Intersection
Weasleys & Gryffindors
# {'Fred', 'George', 'Ron', 'Ginny'}

## Union
Weasleys | Gryffindors
# {'Ron', 'Hermine', 'George', 'Harry', 'Ginny', 'Seamus', 'Fred'}

## Difference
Gryffindors - Weasleys
# {'Harry', 'Hermine', 'Seamus'}

## Symmetric Difference
Gryffindors ^ {'Harry', 'Ginny', 'Malfoy'}
# {'Ron', 'Fred', 'George', 'Malfoy', 'Hermine', 'Seamus'}

## Set Disjoint
Gryffindors.isdisjoint({'Malfoy', 'Grabbe', 'Goyle'})
# True
```

```python
## Subset
Weasleys.issubset(Gryffindors)
# True

## Superset
Gryffindors.issuperset(Weasleys)

## Pop, xóa và trả về phần tử ngẫu nhiên
print(Gryffindors.pop())
# 'Seamus'
```

{{< admonition type=notes title="Set và List" open=true >}}
Khi chỉ cần kiểm tra một phần tử có nằm trong một tập hợp nào đó hay không, hoặc lưu trữ các giá trị không lặp lại mà không cần quan tâm đến thứ tự, chúng ta nên dùng Set. Ngược lại, thì dùng List.  
{{< /admonition >}}

## 5. Dictionaries

Dictionary là một tập hợp của các đối tượng có dạng - `key:value`, trong đó:

- Mỗi key sẽ có một hoặc nhiều giá trị tương ứng.
- Các key là duy nhất và có kiểu dữ liệu immutable.
- Values có kiểu dữ liệu mutable.

### 5.1. Tạo dict

Có hai cách cơ bản để tạo dict, một là sử dụng `{key:value}`, hai là sử dụng hàm `dict()`.

```python
# Sử dụng {}
names_and_countries = {'Adam': 'Argentina',
                       'Beth': 'Bulgaria',
                       'Charlie': 'Colombia',
                       'Dani': 'Denmark',
                       'Ethan': 'Estonia'}

# Sử dụng dict()
names_and_countries = dict(Adam = 'Argentina',
                           Beth = 'Bulgaria',
                           Charlie = 'Colombia',
                           Dani = 'Denmark',
                           Ethan = 'Estonia')

names_and_countries = dict([('Adam', 'Argentina'),
                            ('Beth', 'Bulgaria'),
                            ('Charlie', 'Colombia'),
                            ('Dani', 'Denmark'),
                            ('Ethan', 'Estonia')])

# Python list to dict
# Keys are names, values are countries
names = ['Adam', 'Beth', 'Charlie', 'Dani', 'Ethan']
countries = ['Argentina', 'Bulgaria', 'Colombia', 'Denmark', 'Estonia']
names_and_countries = dict(zip(names, countries))
```

### 5.2. Truy cập các giá trị

Chúng ta cũng có hai cách để truy cập vào các giá trị trong dict:

- Sử dụng `[key]`
- Sử dụng phương thức `get()`

```python
# Get value for the key 'Adam'
names_and_countries['Adam']
names_and_countries.get('Adam')

# Get value for the key 'Charlie'
names_and_countries['Charlie']

# Nếu k tồn tại key, [] sẽ trả về lỗi, get trả về None
names_and_countries.get('Zoe')

# Second argument returned if key not in dictionary
# Returns value if key in dictionary
names_and_countries.get('Zoe', 'Name not in dictionary')
```



### 5.3. Các thao tác với dict

```python
# Thêm phần tử vào dict
my_dict['new_key'] = 'new_value'

# Thay đổi giá trị
my_dict['key_name'] = 'new_value

# Xóa phần tử
del my_dict['key_name']

# shallow copy
shallow_copy = my_dict.copy()

# Deep copy
import copy
deep_copy = copy.deepcopy(my_dict)

# Membership 
key_name in my_dict
```

```python
# keys, values and items
>>> names_and_countries.keys()
dict_keys(['Adam', 'Beth', 'Charlie', 'Dani', 'Ethan', 'Fred'])
 
>>> names_and_countries.values()
dict_values(['Argentina', 'Bulgaria', 'Colombia', 'Denmark', 'Estonia', 'France'])
 
>>> names_and_countries.items()
  
dict_items([('Adam', 'Argentina'), 
            ('Beth', 'Bulgaria'), 
            ('Charlie', 'Colombia'), 
            ('Dani', 'Denmark'), 
            ('Ethan', 'Estonia'), 
            ('Fred', 'France')])
```

### 5.4. Một số phương thức

- `dict.clear()`: Xóa tất cả các phần tử trong dict.
- `dict.update(dict2)`: Merge hai dict, nếu có cùng key thì giá trị tương ứng với key trong dict sẽ bị thay thế bởi key trong dict2.
- `dict.pop()`: Xóa một key và trả về giá trị của nó.
- `dict.popitem()`: Xóa một cặp `key-value` ngẫu nhiên và trả về nó ở định dạng tuple.

Ví dụ với `update()`

```python
# Ví dụ 1
A = dict(a = 1, b = 2)
B = dict(c = 3, d = 4)
A.update(B)

# Có cùng key
A = dict(a = 1, b = 2)
B = dict(b = 100)
A.update(B)

# More examp
A = dict(a = 1, b = 2)
B = [('c', 3), ('d', 4)]
A.update(B)

# More more
A = dict(a = 1, b = 2)
A.update(c = 3, d = 4)
```

### 5.5. setdefault và defaultdict

`setdefault` sẽ trả về giá trị hiện tại nếu nó tồn tại, ngược lại sẽ gán cho nó một giá trị mặc định.

Ví dụ, chúng ta có Ba người bạn Adam, Bella và Cara đã đi ăn tối với nhau. Các món ăn mà họ gọi và mức giá tương ứng được lưu trữ trong các list khác nhau.

```python
people = ['Adam', 'Bella', 'Cara',
          'Adam', 'Bella', 'Cara',
          'Adam', 'Bella', 'Cara',]
 
food = ['soup', 'bruschetta', 'calamari',   # starter
        'burger', 'calzone', 'pizza',       # main
        'coca-cola', 'fanta', 'water']      # drink
 
# Cost of each item in £
prices = [3.20, 4.50, 3.89,
          12.50, 15.00, 13.15,
          3.10, 2.95, 1.86]
 
# Zip data together to allow iteration
# We only need info about the person and the price
meal_data = zip(people, prices)
```

Bây giờ, ta phải tính số tiền mỗi người phải trả:

```python
# Sử dụng get
total = {}
for (person, price) in meal_data:
 
    # get method returns 0 the first time we call it
    # and returns the current value subsequent times
    total[person] = total.get(person, 0) + price
```

```python
# Sử dụng setdefault
meal_data = zip(people, prices)
individual_bill = {}
 
for (person, price) in meal_data:
 
    # Set default to empty list and append in one line!
    individual_bill.setdefault(person, []).append(price)
```

`defauldict` là một dictionary trả về giá trị mặc định tùy theo kiểu dữ liệu khai báo ban đầu khi không tìm thấy key trong dict. Chúng ta thực hiện lại hai ví dụ trên sử dụng _defaultdict_:

```python
# Import from collections module
from collections import defaultdict
meal_data = zip(people, prices)
total = defaultdict(int)
individual_bill = defaultdict(list)

for (person, price) in meal_data:
    total[person] += price
    individual_bill[person].append(price)
````
