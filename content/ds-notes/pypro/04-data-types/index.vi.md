---
title: "Pypro - Kiểu dữ liệu"
subtitle: ""
slug: python-data-types
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
Trước khi đi tìm hiểu về các kiểu dữ liệu trong Python, ta cần làm quen với hai khái niệm:

- Immutable: Đây là kiểu dữ liệu bất biến, chúng ta không thể thêm/sửa/xóa giá trị sau khi tạo. Ví dụ: *int, float, complex, bool, None, str, tuple, frozenset*
- Mutable: Ngược lại với trên, chúng ta có thể thực hiện các thao tác thêm/sửa/xóa. Ví dụ: *list, set, dict*

## 1. Kiểu dữ liệu số

Trong Python, có ba kiểu dữ liệu số:

- Số nguyên (int)
- Số thực (float)
- Số phức (complex)

### 1.1. Tạo dữ liệu kiểu số

```python
# Số nguyên
my_int = 42
print(type(my_int)) # <class 'int'>

# Số thực
my_float = 3.0 
print(type(my_float)) # <class 'float'>

# Số phức
my_complex = 4.22 + 20j
my_complex = complex(4.22, 20)
print(my_complex) # (4.22+20j)
```

### 1.2. Một số hàm với dữ liệu số

```python
# returns maximum from n numbers(n > 2)
max(30, 20) # 30
# returns minimum from n numbers(n > 2)
min(30, 20) # 20
# returns absolute value of a number
abs(-50) # 50
# returns a rounded to decimal value of a number
round(my_float) # 3
# returns the power of a number, similar to using '**' operator, eg "10**2" 
pow(10, 2) # 100
# returns quotient and remainder of integer division
divmod(6, 4) # (1, 2)
# convert a number to a hexadecimal number
hex(42) # 0x2a
```

### 1.3. Chuyển đổi giữa các kiểu dữ liệu

```python
my_int = 42
my_float = 3.0

# int to str
str(my_int) # 42
# int to float
float(my_int) # 42.0
# float to int
int(my_float) # 3
# float to str
str(my_float) # 3.0
```

## 2. Kiểu dữ liệu chuỗi

Trong Python, string là:

- Một tập hợp các chuỗi ký tự 
- Nó có dạng immutable

### 2.1. Tạo một chuỗi

```python
# Single Quote: insert string value inside single inverted commas  
text = 'strings can be single quoted'

# Double Quote: can be useful for escaping single inverted comma(') rest there is no difference
text = "strings can be double quoted" 

# Triple Quote: used for multi-line text, can be used with single/double inverted commas
text = """This is a long text.
        And want to use multiple lines."""
```

### 2.2. Một số kiểu string

```python
# normal str, escaping characters
print("normal str,\t escaping characters") 

# \n raw string \t no escaping characters
print(r"\n raw string \t no escaping characters")

# unicode type, it represents english and non-english characters
print(u"This is unicode")
```

### 2.3. Định dạng chuỗi

```python
# formatting type
n = 1

# or C like formatting
text = "This is a String number %s" %n

# or f-string to pass variable
text = f"This is a String number {n}"
text = f"This is a String number {n = }"

# or even to pass expression
text = f"This is a String number {20-19}" 

# or format method of string
text = "This is a String number {0}".format(n) 
```

### 2.4. Toán tử

```python
# Toán tử lặp *
string1 = "this" * 5
print(string1) # thisthisthisthisthis

# toán tử nối +
string1 = "This is 1."
string2 = "This is 2."
new_string = string1 + string2
print(new_string) # This is 1.This is 2.
```

### 2.5. Indexing, iterating và slicing

```python
sample_str = "This contain some characters"

## Indexing: accessing item/character from string
print(sample_str[0]) # T
print(sample_str[2]) # i

# negative indexing: starts from 1 and not 0
print(sample_str[-1]) # s
print(sample_str[-5]) # c
```

```python
## Iterating: going over item by item from a string
for x in sample_str:
  print(x)
```

```python
## Slicing: for creating substrings, syntax is [start_index:end_index:step] 
# start_index is starting index of substring, default is 0
# end_index is ending index, (end_index - 1) is considered, default is last index
# step is the gap between characters, default is 1 
my_string = "This is some string."
print(my_string[5:7]) # is
print(my_string[5:]) # is some string.
print(my_string[:4]) # This 
print(my_string[:5:2]) # Ti 
print(my_string[:-4]) # This is some str
# reverse a string
print(my_string[::-1]) # .gnirts emos si sihT
```

### 2.6. Một số phương thức với string

```python
my_string = "this IS it."

print(my_string.lower()) # this is it.
print(my_string.upper()) # THIS IS IT.
print(my_string.capitalize()) # This is it.

# Splits at a given string key(which is whitespace here) and returns list of strings
print(my_string.split(" ")) # ['this', 'IS', 'it.']

# Removes whitespace from beginning, also can strip given another key string 
print(my_string.strip()) # this IS it.

# Searches given key/string(which is 'it' here) and returns starting index if found
print(my_string.index("it")) # 8

# Searches given key string(which is 'it' here), replaces with 
# second key(which is 'not it' here) string and then returns the final string
print(my_string.replace("it","not it")) # this IS not it.

# joins a list of strings to a single string with a given string key(which is '.' here)
print(".".join(['hey','is','this','it?'])) # hey.is.this.it?
```

### 2.7. Một số hàm với string

```python
my_string = "this IS it."

# Returns the length of a string
print(len(my_string)) # 11

# Returns the string representation of any object, for str object returns a string with no escaping characters
print(repr("This \t should have escaped.")) # 'This \t should have escaped.'

# Returns a Unicode of a character
print(ord("c")) # 99 

# Returns Converted the Unicode to a character
print(chr(ord("c"))) # c
```

### 2.8. Encoding và Decoding

```python
# s: string obj
s = "This is üŋíc0de"  # unicode string: code points

# encoding
# encoded_s: byte obj
encoded_s = s.encode('utf-8') # -> b'This is \xc3\xbc\xc5\x8b\xc3\xadc0de'

# decoding
encoded_s.decode('utf-8') # 'This is üŋíc0de'
```

### 2.9. Chuyển đổi kiểu

```python
my_string = "bar"
my_string1 = "20"

# str to int
print(int(my_string)) # ValueError
print(int(my_string1)) # 20

# str to float
print(float(my_string)) # ValueError
print(float(my_string1)) # 20.0

# str to bytes
print(bytes(my_string, encoding='utf-8')) # b'bar'
```


## 3. Kiểu dữ liệu Boolean

Đây là kiểu dữ liệu chỉ gồm hai giá trị *True* và *False*. Về cơ bản *False* có thể tương đương với giá trị `0`, ngược lại là `True`.

### 3.1. Tạo kiểu bool

```python
my_bool = True
print(type(my_bool)) # <class 'bool'>

my_bool = my_bool + 4 # becomes 5

my_bool = False
my_bool = my_bool + 4 # stays 4
```

### 3.2. Chuyển đổi kiểu

```python
# number to bool, anything not 0 is True
print(bool(-40), bool(0), bool(40)) # True False True

# str to bool, empty string is False, rest is True
print(bool(""), bool("This is string")) # False True
```

## 4. Kiểu dữ liệu byte

### 4.1. Hàm bytes()

```python
## create a bytes object
data = bytes("This is bytes data", 'UTF-8')
print(data) # b'This is bytes data'

# or can use b prefix on string like syntax
print((b'42')) # b'42'
print(type(b'42')) # <class 'bytes'>

## initialize bytes object with 0's by providing size in int
my_bytes = bytes(4)
print(my_bytes) # b'\x00\x00\x00\x00'

## indexing a bytes object returns a Unicode of a character
print(data[0], chr(data[0])) # 84 T

## create bytes object using a iterable objects
print(bytes([1,2,3])) # b'\x01\x02\x03'
print(bytes((80,50,60))) # b'P2<'
```

### 4.2. Hàm bytearray()

```python
# create bytearray with 0's by providing size in int
output = bytearray(4)

print(output) # bytearray(b'\x00\x00\x00\x00')
print(type(output)) # <class 'bytearray'>

## bytearray is mutable so
output[0] = 30
print(output) # bytearray(b'\x1e\x00\x00\x00')
```

## 5. Đối tượng None

*None* là một hằng số đặc biệt, có kiểu *NoneType*, dùng để biểu thị một giá trị null (không có giá trị), hoặc một khoảng trống rỗng.

```python
n = None
print(type(None)) # <class 'NoneType'>

# Kiểm tra 
n is None

# None trong câu lệnh if, None is False
if n: # same as "if n != None:"
  print('will not enter this condition')

## not to negate that condition
if not n: # same as "if n == None:"
  print('will enter this condition, as n is None')
```

## 6. Một số hàm làm việc với kiểu dữ liệu

### 6.1. Hàm type(obj)

Hàm này được sử dụng để kiểm tra kiểu dữ liệu của một đối tượng.

```python
a = "What?"
print(type(a)) # str

b = 5.0
print(type(b)) # float
```

### 6.2. Hàm isinstance(object, class)

Hàm này được sử dụng để kiểm tra xem một đối tượng có phải là một thể hiện của một lớp nào đó hay không.

```python
a = 23
print(isinstance(a, int)) # True
print(isinstance(a, float)) # False
print(isinstance(a, str)) # False
```

### 6.3. Hàm id(obj)

Hàm này, xác định địa chỉ của một đối tượng được tạo ra trong bộ nhớ.

```python
my_float = 50.0

# object id will differ each time with program
print(id(my_float)) # 1875526208176
```

### 6.4. Hàm dir(obj)

Hàm này trả về một list các tên của các biến, hàm, class trong một đối tượng.



```python
# Ví dụ:
print(dir(int))
```

    ['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'as_integer_ratio', 'bit_count', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
    
