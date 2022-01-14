---
title: "Pypro - Numbers và Strings"
subtitle: ""
slug: python-number-and-string
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
## 1. Numbers

### 1.1. Định dạng số thực

```python
x = 211911461911461819112146
y = 2**70
z = x / y # 179.4959901398329

# Sử dụng format
print(':.2f'.format(z))

# Sử dụng hàm round()
round(z, 2)

# Sử dụng hàm format
format(z, '.2f')

# Sử dụng f-string
f'{z:.2f}'
```

### 1.2. So sánh hai số thực

```python
# Vấn đề:
# Python sử dụng cơ chế làm tròn số nên
x = 0.1 + 0.1 + 0.1
y = 0.3
x == y # False

# Sử dụng math.isclose(a, b, *, rel_tol=1e-09, abs_tol=0.0)
# rel_tol: chênh lệch tương đối
# abs_tol: chênh lệch tuyệt đối
# abs(a-b) <= max(rel_tol * max(abs(a), abs(b)), abs_tol)
import math
math.isclode(x, y)
```

### 1.3. Số phức

```python
# Số phức
a = 5 + 7j
complex(5, 7)

# Số phức liên hợp
a.conjugate()

# Phần thực, phần ảo
a.imag
a.real
```


## 2. Strings

### 2.1. Định dạng strings

**Sử dụng phương thức format**

```python
# Sử dụng {}
'{} % {} = {}'.format(10, 3, 10 % 3)

# Sử dụng {number}
'{1} % {2} = {0}'.format(10 % 3, 10, 3)

# Sử dụng {name}
'{a} % {b} = {mod}'.format(a=10, b=3, mod=10 % 3)
```

**Sử dụng *f-string***

```python
# Sử dụng tên
a = 10
b = 3
f'{a} % {b} = {a % b}' 
f'{a = }'
```

**Một số ký tự đặc biệt**

| Ký tự | Ý nghĩa |
|--|--|
| `:nd` | Định dạng số nguyên |
| `:c` | Ký tự tương ứng với số nguyên|
| `:s` | Mặc định là s - string |
| `:.nf` | Định dạng số thực |
| `:ne` | $a * 10^x$ |
| `:<nd`| Căn trái |
| `:^nd`| Căn giữa |
| `:>nd`| Căn phải |
| `:+0nd`| Thêm dấu `+` và số `0` vào vị trí trống trước số nguyên |
| `:,d` | Thêm dấu `,` đối với phần nguyên |

### 2.2. Phép nối và phép lặp

Toán tử `+` được sử dụng để nối các chuỗi với nhau.

Toán tử `*n` được sử dụng để lặp lại một chuỗi n lần

```python
s1 = 'happy'
s2 = 'birthday'

s1 + ' ' + s2 # 'happy birthday'
s1 * 3 # 'happyhappyhappy'
```

### 2.3. Loại bỏ khoảng trắng

Sử dụng phương thức `strip()`

```python
# strip, rstrip, lstrip
sentence = '\t \n This is a test string. \t\t \n'
sentence.strip() # Xóa tất cả khoảng trắng
sentence.ltrip() # Xóa khoảng trắng ở đầu chuỗi
sentence.rtrip() # Xóa khoảng trắng ở cuỗi chuỗi
```

### 2.4. Chuyển đổi ký tự

Một số phương thức giúp chuyển đổi giữa ký tự in hoa và in thường:

```python
my_str = 'happy birthday'
my_str.upper() # 'HAPPY BIRTHDAY'
my_str.lower() # 'happy birthday'
my_str.title() #'Happy Birthday'
my_str.capitalize() # 'Happy birthday'
my_str.swapcase()
```

## 3. Substrings

### 3.1. Tìm kiếm

```python
sentence = 'to be or not to be that is the question'

# Đếm số lần xuất hiện substr, count(substr, start_index, end_index)
sentence.count('to') # 2

# Tìm vị trí xuất hiện, index, rindex, find, rfind
sentence.index('be')

# Kiểm tra xem substr có nằm trong str không
'that' in sentence # True

# Kiểm tra chuỗi ký tự bắt đầu, kết thúc
sentence.startswith('to')
sentence.endswith('Quest')
```

### 3.2. Thay thế

```python
# Cú pháp
my_str.replace('old_substr', 'new_substr')
```

## 4. Split và Join

Phương thức `split()`

```python
# split, rsplit('chr', number)
letters = 'A, B, C, D'
letters.split(', ')     # ['A', 'B', 'C', 'D']
letters.split(', ', 2)  # ['A', 'B', 'C, D']
```

Phương thức `partition()` và `rpartition()`: Tách một chuỗi thành ba phần.

```python
my_str = 'Amanda: 89, 97, 92'
my_str.partition(': ') # ('Amanda', ': ', '89, 97, 92')
```

Phương thức `splitlines()`: Tách một đoạn văn thành nhiều dòng.

```python
lines = 'This is line 1\nThis is line2\nThis is line3'
lines.splitlines() # ['This is line 1', 'This is line2', 'This is line3']

# splitlines(True) nếu muốn giữ lại \n
lines.splitlines(True) # ['This is line 1\n', 'This is line2\n', 'This is line3']
```

Phương thức `join()`: Nối các substr với nhau.

```python
# Join
letters_list = ['A', 'B', 'C', 'D']
','.join(letters_list) # 'A,B,C,D'
```


## 5. Raw string

Raw string, là một chuỗi mà trong đó các ký tự đặc biệt như `\` sẽ là chính nó mà không mang ý nghĩa đặc biệt nào khác.

```python
# string
file_path = 'C:\\MyFolder\\MySubFolder\\MyFile.txt'

# raw string
file_path = r'C:\MyFolder\MySubFolder\MyFile.txt'
```

## 6. Biểu thức chính quy

### 6.1. Ký tự đặc biệt

| Ký tự | Ý nghĩa |
|--|--|
| . | Một ký tự bất kỳ, ngoại trừ newline |
| \\. | Dấu `.` |
| \d | Một số |
| \D | Không phải một số |
| \w | Một ký tự alphanumeric `[a-zA-Z0-9_]` |
| \W | Ngược lại với \w |
| \s | Một khoảng trắng |
| \S | Không phải một khoảng trắng |
| \bfoo | Một từ bắt đầu bằng foo|
| foo\b | Một từ kết thúc bằng foo|
| \Bf | Ngược lại với \b|
| str\Z | Một chuỗi có kết thúc bằng str|
| \Astr | Mỗi chuỗi có bắt đầu bằng str|
| \n | newline |
| \t | tab |

### 6.2. Ký tự nhóm

| Ký tự | Ý nghĩa |
|--|--|
| ^ | Bắt đầu một dòng |
| $ | Kết thúc một dòng |
| ab\|cd | Khớp với `ab` hoặc `cd`|
| [ab-d] | Khớp với một ký tự trong: `a, b, c, d`|
| [^ab-d] | Khớp với các ký tự ngoại trừ: `a, b, c, d`|
| () | sub-patterns |

### 6.3. Ký tự lặp

| Ký tự | Ý nghĩa |
|--|--|
| + | Lặp lại >= 1 lần |
| * | Lặp lại >= 0 lần |
| ? | Lặp lại 0 hoặc 1 lần |
| [ab]{2} | a hoặc b lặp lại 2 lần |
| [ab]{2, 5} | a hoặc b lặp lại số lần >=2, <=5 |
| [ab]{2, } | a hoặc b lặp lại >=2 lần |

## 7. Module re

### 7.1. Một số phương thức cơ bản

| Phương thức | Ý nghĩa |
|--|--|
|re.findall(pattern, str)| Trả về một list các substr khớp với pattern|
|re.split(pat, str, maxsplit = 0)| Trả về một list các substr được phân tách bởi pattern|
|re.sub(pat, replace, str, count = 0)| Tìm kiếm và thay thế|
|re.subn()| Tương tự như re.sub(), nhưng trả về một tuple (new_str, num_of_sub)|

### 7.2. Đối tượng match

Phương thức `re.search(pattern, str)` sẽ tìm kiếm, nếu nó tìm thấy chuỗi khớp với kết quả nó sẽ trả về một đối tượng *match* và dừng tìm kiếm. Nếu không tìm thấy, sẽ trả về `None`.

| Phương thức | Ý nghĩa |
|--|--|
|match.group(n)| Trả về một phần của kết quả khớp được, mặc định là tất cả |
|match.start()| Trả về vị trí xuất hiện đầu tiên của chuỗi khớp được|
|match.end()| Trả về vị trí xuất hiện cuối cùng của chuỗi khớp được|
|match.span()| Kết hợp `start()` và `end()`|
|match.re| Trả về *pattern* trong phương thức *search*|
|match.string| Trả về *string* trong phương thức *search*|

### 7.2. Ví dụ

**Ví dụ 1: Tìm kiếm với findall**


```python
# Import module re
import re

# my string
string = 'hello 12 hi 89. Howdy 34'

# Pattern, tất cả các số
pattern = '\d+'

# findall
result = re.findall(pattern, string) 
print(result)

```

    ['12', '89', '34']
    

**Ví dụ 2: Tách chuỗi với split**


```python
string = 'Twelve:12 Eighty nine:89.'
pattern = '\d+'
result_1 = re.split(pattern, string) 

# maxsplit = 1
# split only at the first occurrence
result_2 = re.split(pattern, string, 1) 

print(f'{result_1 =}\n{result_2 =}')
```

    result_1 =['Twelve:', ' Eighty nine:', '.']
    result_2 =['Twelve:', ' Eighty nine:89.']
    

**Ví dụ 3: Tìm kiếm và thay thế**


```python
# string
string = 'abc 12de 23 \n f45 6'

pattern = '\s+'  # matches all whitespace characters
replace = ''     # empty string

sub_str = re.sub(pattern, replace, string) 
subn_str = re.subn(pattern, replace, string) 
print(f'{sub_str = }\n{subn_str = }')

```

    sub_str = 'abc12de23f456'
    subn_str = ('abc12de23f456', 4)
    

**Ví dụ 4: search và match**


```python
# my string
string = '39801 356, 2102 1111'

# Three digit number followed by space followed by two digit number
pattern = '(\d{3}) (\d{2})'

# match variable contains a Match object.
match = re.search(pattern, string) 

# result
str_match = match.group()
group_1 = match.group(1)
group_2 = match.group(2)
match_start = match.start()
match_end = match.end()
match_span = match.span()
```
