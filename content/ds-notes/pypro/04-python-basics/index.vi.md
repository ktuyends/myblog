---
title: "Pypro - Làm quen với Python"
subtitle: ""
slug: basic-python
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
## 1. Biến và các kiểu dữ liệu

### 1.1. Biến

Trong Python, mọi thứ đều là đối tượng, và một biến chỉ đơn giản là một tên, mang ý nghĩa tượng trưng, trỏ đến một đối tượng trong bộ nhớ. 

Ví dụ:

```python
# Phép gán
my_var = 100

# xem địa chỉ trong bộ nhớ của my_var
id(my_var)
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

### 1.2. Các kiểu dữ liệu

Trong Python, có nhiều kiểu dữ liệu như *integer (số nguyên), floats (số thực), strings (chuỗi các ký tự),...*

Chúng ta sử dụng hàm `type(obj)` để kiểm tra kiểu dữ liệu của một đối tượng.

**Số nguyên - integer**


```python
# my_int
my_int = 10

# print
print(my_int, type(my_int), id(my_int))
```

    10 <class 'int'> 3173282480656
    

**Số thực - floats**




```python
# my_float
my_float = 7.5

# print
print(my_float, type(my_float))
```

    7.5 <class 'float'>
    


```python
# Làm tròn
print(format(my_float, '0.5f'))
```

    7.50000
    

**Booleans**

Trong Python, Bool là kiểu dữ liệu chỉ có hai giá trị:

- False - Tương đương với giá trị 0
- True - Tương đương với các giá trị khác 0


```python
# my_bool
my_bool = True

# So sánh
my_bool == 1
```




    True



**Số phức - complex**

Số phức, có cú pháp: `a + bj`

```python
# Tạo số phức
my_complex = 10 + 7j
```

**Kiểu None**

None là một đối tượng đặc biệt trong Python mà ta có thể hiểu là không có gì, nó giống như một tập hợp rỗng trong toán học.

```python
# NoneType
my_var = None
```

### 1.3. Comment và ngắt dòng

```python
# Viết comment sau dấu #

"""
Đôi khi có thể 
Viết comment trên nhiều dòng 
Như thế này
Ví dụ docstring
"""
```

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



## 2. Cấu trúc dữ liệu

Trong python, có nhiều kiểu dữ liệu còn được gọi là *container* - đây là các kiểu dữ liệu tập hợp nhiều giá trị, mỗi giá trị là một đối tượng và có một kiểu dữ liệu, có thể giống nhau hoặc khác nhau.

Một số kiểu trong nhóm này là *mutable* - nghĩa là ta có thể tùy ý thêm, sửa, xóa các phần tử bên trong nó.

Một số kiểu còn lại thuộc nhóm *immutable* - nghĩa là ta không thể thêm, sửa hoặc xóa các phần tử bên trong nó.

### 2.1. List

List là một cấu trúc dữ liệu, chứa nhiều phần tử khác nhau, trong đó mỗi phần tử có một vị trí xác định mà ta có thể truy xuất dựa vào vị trí của nó.

```python
# Tạo một list rỗng
my_list1 = []
my_list2 = list()

# Tạo một list
my_list = [1, 2, 3]

# Lấy các phần tử bên trong list
my_list[0] # 1
my_list[1] # 2

# Xem số lượng phần tử bên trong list
len(my_list)
```

Thay đổi các phần tử bên trong list:

```python
# Chỉnh sửa giá trị
my_list[0] = 100 # [100, 2, 3]

# Xóa phần tử
del my_list[0] # [2, 3]

# Thêm phần tử
my_list.append(4) # [2, 3, 4]
```

### 2.2. Tuple

Chúng ta có thể nghĩ về tuple như các list immutable:

```python
# Tạo tuple rỗng
my_tuple = ()
my_tuple = tuple()

# Tạo tuple chỉ có một phần tử
my_tuple = (5, )

# Tạo tuple
my_tuple = (5, 10, 15)

# Tạo tuple có thể không cần dấu ()
one_tuple = 5, 
my_tuple = 5, 10, 15
```

### 2.3. Strings

String là một tập các ký tự, tạo thành một từ, một câu, hoặc một đoạn văn,...Mỗi ký tự trong string đều có một vị trí xác định.

```python
# Tạo string
my_str1 = 'Hà Nội, hôm nay trời mưa'
my_str2 = "Ngày mai, là một ngày mới"

my_str3 = """Đây là một đoạn string
             Được viết trên nhiều dòng"""
```



```python
# Một string phức tạp
# Sử dụng cả "" và '', \t = tab, \n = newline
a = "I'm a lumberjack\tand I'm OK\nI sleep all night\tand I work all day."
print(a)
```

    I'm a lumberjack	and I'm OK
    I sleep all night	and I work all day.
    

Strings thuộc nhóm immutable, ta có thể trích xuất các phần tử của nó nhưng không thể sửa đổi các ký tự bên trong nó. Mọi hành động sửa đổi sẽ tạo thành một chuỗi mới.

### 2.4. Sets

Với Set, chúng ta có thể nghĩ nó như một tập hợp trong toán học. Mà trong một tập, thì các phần tử không có thứ tự xác định và có giá trị là duy nhất. Vì các phần tử không có thứ tự nên ta cũng không thể lấy ra các giá trị bên trong Set dựa vào vị trí của nó.

```python
# Tạo một set rỗng
my_set = set()

# Tạo một set
my_set = {5, 10, 15}

# Thêm phần tử
my_set.add(20) # {5, 10, 15, 20}

# Xóa phần tử
my_set.remove(20)

# Phương thức pop() xóa phần tử và trả về giá trị bị xóa
my_set.pop()
```



### 2.5. Dictionary

Dictionary là một tập hợp của các cặp đối tượng có dạng: *key:value*, trong đó *key* là các đối tượng thuộc nhóm immutable và duy nhất.

Dictionary thuộc nhóm mutable.

```python
# Tạo dict rỗng
my_dict = {}
my_dict = dict()

# Tạo dict
my_dict = {'a': 1, 'b': 2, 'c': 3}

# Danh sách
my_dict.keys()
my_dict.values()
my_dict.items()

# Lấy các phần tử dict[key]
my_dict['a']
my_dict.get(key) # Trả về None nếu k tìm thấy
my_dict.get(key, 'N/A') # Trả về N/A nếu k tìm thấy

# Thêm phần tử
my_dict[new_key] = new_value

# Xóa phần tử
my_dict.pop(key)
my_dict.pop(key, 'N/A') # Trả về N/A nếu không tồn tại key
del my_dict[key]
my_dict.popitem() # Xóa ngẫu nhiên
```

## 3. Toán tử

### 3.1. Các toán tử

- Toán tử cơ bản: *+, -, \*, /*
- Toán tử nối: `+` nối các tuple/list/str với nhau
- Toán tử lặp: `*` tương tự như toán tử nối, nhưng mang ý nghĩa khác
- Phép chia lấy phần nguyên: *a // b*
- Phép chia lấy phần dư: *a % b*
- Toán tử tập hợp: *& (phép giao), | (phép hợp), - (phép trừ), ^ (hiệu số đối xứng)*
- Toán tử so sánh: *==, !=, >, >=, <, <=*
- So sánh về mặt đối tượng: *is, is not*
- Toán tử boolean: *and, or, not, and not, or not*
- Toán tử: *in, not in*

### 3.2. Một số lưu ý

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

{{< admonition type=notes title="So sánh hai số thực" open=true >}}
Toán tử `==` khi so sánh kiểu dữ liệu int và bool không có vấn đề, nhưng với kiểu floats sẽ không chính xác vì Python sử dụng cơ chế làm tròn.

```python
0.1 == 0.1 # True
0.1 + 0.2 == 0.3 # False
```
{{< /admonition >}}

{{< admonition type=notes title="Đối tượng singleton" open=true >}}
Theo mặc định các số nguyên từ -5 đến 256 (đối tượng singleton) được Python tạo sẵn, vì vậy nó có địa chỉ xác định. Nên khi ta sử dụng toán tử `is` để so sánh hoặc sử dụng `id(num)` để kiểm tra vị trí thì nó luôn cố định.

Một số đối tượng singleton khác như: *True, False, None*.

Với những đối tượng này, ta nên sử dụng toán tử `is` thay vì sử dụng `==`.
{{< /admonition >}}

{{< admonition type=notes title="Kiểu boolean" open=true >}}
Khi nhắc đến kiểu dữ liệu boolean, mọi thứ biểu thị giá trị `0`, rỗng, `None`,...sẽ được hiểu là False. Ngược lại là True.

```python
bool(0), bool(-1), bool(1), bool(100) # (False, True, True, True)
bool(None) # False
```
{{< /admonition >}}

## 4. Cấu trúc điều khiển

### 4.1. Câu lệnh if

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

### 4.2. Vòng lặp for

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

### 4.3. Vòng lặp while

```python
# Cú pháp
while <dieu_kien>:
    # Thực thi cho đến khi điều kiện trả về False

else: # Có thể có hoặc không
    # Nếu vòng lặp không bị break
    # Thì thực thi else sau khi kết thúc vòng lặp 
```

### 4.4. break, continue và pass

- break: thoát khỏi vòng lặp
- continue: thoát khỏi lượt lặp hiện tại, chuyển sang lượt lặp tiếp theo
- pass: Không thực thi gì hết, chỉ mang ý nghĩa giữ chỗ

> Nếu sử dụng câu lệnh `try-finally` bên trong vòng lặp, thì `finally` luôn luôn thực thi, dù cho vòng lặp gặp phải break hoặc continue.

### 4.5. enumerate và zip

```python
# zip()
a = ['a', 'b', 'c']
b = [5, 10, 15]
zip(a, b) # [('a', 5), ('b', 10), ('c', 15)]

# enumerate
my_list = ['monday', 'tuesday', 'sunday']
enumerate(my_list) # [(0, 'monday'), (1, 'tuesday'), (2, 'sunday')]
```

## 5. Imports

```python
# import một module
import math

# Sử dụng module
math.pi
math.sin(math.pi)

# Alias
import numpy as np
np.array([1, 2, 3, 4, 5])

# from module import
from math import sin, pi
pi
sin(pi)
```

## 6. Functions

Functions trong Python là một khối các câu lệnh thực hiện một hoặc nhiều nhiệm vụ nào đó.

```python
# Tạo hàm
# param1, param2,...là các tham số, các tham số có thể có giá trị mặc định
# return: Trả về kết quả, hàm có thể không trả về kết quả
def my_func(param1, param2, param3 = default_value):
    # Tập hợp các câu lệnh
    return my_results

# Gọi hàm, arg3 nếu k được truyền sẽ sử dụng default_value
my_func(arg1, arg2, [arg3])
```

Hàm ẩn danh: là một hàm được định nghĩa trên một dòng, mà không có tên.

```python
# Sử dụng từ khóa lambda
my_func = lambda params: <biểu thức>
```

## 7. Classes

Class là mô tả về một đối tượng nào đó. Một đối tượng thì gồm thuộc tính và phương thức, trong đó:

- Thuộc tính thể hiện các đặc điểm của đối tượng
- Phương thức thì thể hiện các hành động của đối tượng

Ví dụ: Lớp mô tả về con người, sẽ có các thuộc tính như tên, địa chỉ, chiều cao, cân nặng,...và có các phương thức như đi, chạy, nhảy,...

### 7.1. Tạo một lớp đơn giản

```python
# Sử dụng từ khóa class
class Employee:
    # Khai báo biến class
    # Truy cập thông qua: class_name.var, self.var
    raise_amount = 1.04
    num_of_emps = 0

    # Thêm thuộc tính
    # self đại diện cho đối tượng
    # first, last, email, pay là thuộc tính
    def __init__(self, first_name, last_name, pay):
        self.first = first_name
        self.last = last_name
        self.email = first_name + '.' + last_name + '@gmail.com'

        # Đếm số employee
        num_of_emps = num_of_emps + 1

    # Thêm phương thức
    # self là bắt buộc, nó đại diện cho obj
    def fullname(self):
        return '{} {}'.format(self.first, self.last)    

    # Thay đổi giá trị thuộc tính sử dụng biến class
    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amount)

    # Class method
    # Không tác động đến thuộc tính của obj
    # Chỉ tác động đến các biến class
    # cls là bắt buộc, nó đại diện cho class
    @classmethod
    def set_raise_amt(cls, amount):
        cls.raise_amount = amount

    @classmethod
    def from_string(cls, emp_str):
        first, last, pay = emp_str.split('-')
        return cls(first, last, pay)

    # Static method
    # Giống một hàm bình thường, không tác động đến class và object
    # Không có cls, không có self
    @staticmethod
    def is_workday(day):
        if dat.week(day) == 5 or day.week(day) ==6
            return day
        return TRUE

# Tạo các cá thể của lớp Employee
emp_1 = Employee('Anthony', 'Nguyen', 70000)
emp_2 = Employee('Tuyen', 'mfe', 50000)
Employee.raise_amount(1.07)

# print
print(emp_1)
print(emp_1.email)
print(emp_1.fullname())
print(Employee.is_sworkday())
```

### 7.2. Kế thừa

Kế thừa, hiểu một cách đơn giản là ta tạo ra các lớp mới, kế thừa lại các phương thức và thuộc tính của lớp cha. Sau đó, ta có thể sử dụng toàn bộ các phương thức và thuộc tính đó, cũng có thể tạo mới hoặc ghi đè.

```python
# Tạo lớp Developer kế thừa lớp Employee
class Developer(Employee):
    # Ghi đè
    raise_amount = 1.10

    # Thuộc tính
    def __init__(self, first, last, pay, prog_lang):

        # Kế thừa
        # Sử dụng super() hoặc
        # Employee.__init__(self, first, last, pay)
        super().__init__(first, last, pay)

        # Khai báo thuộc tính mới
        self.prog_lang = prog_lang
```

```python
# Tạo lớp Manager
class Manager(Develop):

    # Thuộc tính
    def __init__(self, first, last, pay, employees = None):
        super().__init__(first, last, pay)
        
        if employees is None:
            self.employees = []
        else:
            self.employess = employees

    # Phương thức thêm emp
    def add_emp(self, emp):
        if emp not in self.employees:
            self.employees.append(emp)

    # Phương thức xóa emp
    def add_emp(self, emp):
        if emp in self.employees:
            self.employees.remove(emp)

    # In danh sách nhân viên
    def print_emps(self):
        for emp in self.employees:
            print('-->', emp.fullname())
```

Một số hàm dùng để kiểm tra:

```python
# Xem một obj có phải là một thể hiện của lớp không
isinstance(obj, class_name)

# Xem một lớp có phải là lớp con của lớp khác không
issubclass(subclass_name, class_name)
```

### 7.3. Một số phương thức đặc biệt

Phương thức *\_\_repr\_\_(self)* và *\_\_str\_\_(self)* thay đổi cách hiển thị khi chúng ta `print(class_name)`:

- `str` được sử dụng để hiển thị kết quả đầu ra cho người dùng. Kết quả của hàm `print()`
- `repr` thường được sử dụng cho mục đích gỡ lỗi, kết quả phải rõ ràng, cụ thể. Kết quả của `object`

### 7.4. Property decorators

Ví dụ về class Employee:

```python
class Employee:
    def __init__(self, first, last):
        self.first = first
        self.last = last

    @property
    def email(self):
        return '{}.{}@gmail.com'.format(self.first, self.last)

    # Setter
    def fullname(self):
        return '{}{}'.format(self.first, self.last)

    @fullname.setter
    def fullname(self, name):
        first, last = name.split(' ')
        self.first = first
        self.last = last

    # deleter
    @fullname.deleter
    def fullname(self):
        print('Delete Name!')
        self.first = None 
        self.last = None
```

```python
# create instance
emp = Employee('John', 'Smith')

# Truy cập vào email như thuộc tính, vì có @property
print(emp.email)

# Sửa đổi fullname, setter
emp.fullname = 'Ha Lan'

# Xóa name, deleter
del emp.fullname
```


