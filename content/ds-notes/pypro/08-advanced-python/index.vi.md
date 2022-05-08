---
title: "Pypro - Một số ghi chú khác"
subtitle: ""
slug: python-advanced
date: 2022-03-06
lastmod: 2022-03-06
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
series: [Python Programming]
series_weight: 8
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
## 1. Iterables

Một trong những cấu trúc dữ liệu phổ biến nhất trong Python mà chúng ta chắc chắn sẽ học qua là list. Với list, chúng ta có thể lặp qua các phần tử của nó như sau:


```python
# Tạo list
my_list = [12, 5, 1994]

# Lặp qua các phần tử của list
for element in my_list:
    print(element)
```

    12
    5
    1994
    

Không chỉ với list, trong Python cũng có nhiều kiểu dữ liệu mà chúng ta hoàn toàn có thể lặp qua các phần tử của nó như tuple, dict, string,...


```python
# for với dict
my_dict = {'name': "Andy Kieu", 'age': 28, 'city': 'Hanoi'}
for key in my_dict:
    print(key)
```

    name
    age
    city
    


```python
# for với string
my_str = 'abc'
for c in my_str:
    print(c)
```

    a
    b
    c
    

Chúng ta gọi các đối tượng mà có thể thực hiện vòng lặp thông qua từng phần tử của nó là iterable. Vậy chúng ta có thể tự tạo ra các đối tượng như thế hay không?

Chúng ta sẽ bắt đầu với một class đơn giản:


```python
class Arr:
    def __init__(self):
        self.a = 0
        self.b = 1
        self.c = 2

# Tạo một object
my_var = Arr()

# Xem các thuộc tính
print(f'a: {my_var.a}')
print(f'b: {my_var.b}')
print(f'c: {my_var.c}')
```

    a: 0
    b: 1
    c: 2
    

Bạn đoán xem chúng ta có thể lặp qua các thuộc tính của `my_var` hay không?


```python
for item in my_var:
    print(item)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_2680/261820685.py in <module>
    ----> 1 for item in my_var:
          2     print(item)
    

    TypeError: 'Arr' object is not iterable


Ôi không! như bạn có thể thấy thì `Arr` không phải là một iterable, vì vậy ta cần phải định nghĩa lại `Arr` để nó trở thành iterable với phương thức `__getitem__()`:


```python
class Arr:
    def __init__(self):
        self.a = 0
        self.b = 1
        self.c = 2

    # Xác định thứ tự của các thuộc tính
    def __getitem__(self, item):
        if item == 0:
            return self.a
        elif item == 1:
            return self.b
        elif item == 2:
            return self.c
        raise StopIteration

# Xem thành quả nào
my_var = Arr()
print(f'Phần tử thứ nhất: {my_var[0]}')
print(f'Phần tử thứ hai: {my_var[1]}')

# Thử với vòng lặp for
for item in my_var:
    print(item)
```

    Phần tử thứ nhất: 0
    Phần tử thứ hai: 1
    0
    1
    2
    

Thêm một ví dụ nữa về cách sử dụng `__getitem()__`


```python
class Sentence:
    def __init__(self, text):
        self.words = text.split(' ')

    def __getitem__(self, item):
        return self.words[item]

s = Sentence('This is some form of text that I want to explore')

for word in s:
    print(word)
```

    This
    is
    some
    form
    of
    text
    that
    I
    want
    to
    explore
    

## 2. Iterators

Cho tới nay, chúng ta đã biết một iterable là một đối tượng mà chúng ta có thể lặp qua các phần tử của nó. Nhưng ta có biết cơ chế này hoạt động như thế nào không.


```python
# Giả sử ta có một list
var = ['a', 10, 12.5]

# Trình lặp
it = iter(var)

# Xác định các phần tử
print(next(it))
print(next(it))
print(next(it))
print(next(it))

```

    a
    10
    12.5
    


    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_4936/4164786260.py in <module>
          9 print(next(it))
         10 print(next(it))
    ---> 11 print(next(it))
    

    StopIteration: 



```python
# Sử dụng vòng lặp for
it = iter(var)
for element in it:
    print(element)
```

    a
    10
    12.5
    

Dựa vào ví dụ trên, ta hiểu đơn giản hàm `iter()` nhận vào một đối tượng `iterable` và trả về một đối tượng `iterator`. Sau đó thông qua `next(iterator)`, sẽ tạo ra các phần tử tiếp theo với mỗi lần sử dụng.

Chúng ta có thể định nghĩa cách thức hoạt động của `iter()` và `next()` thông qua phương thức `__iter__()` và `__next__()`. Ví dụ:


```python
# Định nghĩa iterator
class SentenceIterator:
    def __init__(self, words):
        self.words = words
        self.index = 0

    def __next__(self):
        try:
            word = self.words[self.index]

        except IndexError:
            raise StopIteration()

        self.index += 1

        return word

    def __iter__(self):
        return self
```

Sau khi đã có iterator, chúng ta phải định nghĩa lại iterable:


```python
# Định nghĩa iterable
class Sentence:
    def __init__(self, text):
        self.words = text.split(' ')

    def __iter__(self):
        return SentenceIterator(self.words)
```

Các bạn có thấy có gì sai sai ở câu lệnh trên không, chúng ta đã không sử dụng `__getitem__()` mà sử dụng `__iter__()`. Do đó chúng ta không thể truy cập vào các phần tử bằng index, nhưng vòng lặp for vẫn sẽ hoạt động bình thường. Cùng xem kết quả nào:


```python
text = "This is a text to test if our iterator returns values backward"
s = Sentence(text)
s[0]
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_4936/3626104857.py in <module>
          1 text = "This is a text to test if our iterator returns values backward"
          2 s = Sentence(text)
    ----> 3 s[0]
    

    TypeError: 'Sentence' object is not subscriptable



```python
# Với vòng lặp for
for w in s:
    print(w)
```

    This
    is
    a
    text
    to
    test
    if
    our
    iterator
    returns
    values
    backward
    

## 3. Generators

Để định nghĩa một iterator, ta cần phải thực hiện khá nhiều bước ví dụ như `__next__()`, `__iter__()`...Xử lý ngoại lệ với _StopIteration_ khi không còn giá trị được trả về...

Generator hiểu một cách nôm na thì nó là một hàm trả về một đối tượng iterator mà chúng ta có thể lặp lại tại một thời điểm. Generator tạo ra một đối tượng kiểu danh sách, nhưng chúng ta chỉ có thể duyệt qua các phần tử của nó một lần duy nhất vì nó không lưu trữ dữ liệu trong bộ nhớ, mỗi một lần lặp nó sẽ tạo ra phần tử tiếp theo trong dãy.

Để tạo generator, ta sử dụng `yield value` thay vì `return value` trong một hàm. Điểm khác biệt ở đây là `yield` chỉ tạm dừng hàm, còn `return` thì trả về kết quả xong thì thoát khỏi hàm.

Ví dụ:


```python
# Tạo generator với yield
def make_numbers(start, stop, step):
    i = start
    while i<=stop:
        yield i
        i += step

# Kết quả
for i in make_numbers(1, 20, 2):
    print(i)
```

    1
    3
    5
    7
    9
    11
    13
    15
    17
    19
    

Chúng ta có thể định nghĩa lại class _Sentence_ ở trên sử dụng generator thay cho iterator:


```python
class Sentence:
    def __init__(self, text):
        self.words = text.split(' ')

    def __iter__(self):
        for word in self.words:
            yield word

text = "This is a text to test our iterator"
s = Sentence(text)
for w in s:
    print(w)
```

    This
    is
    a
    text
    to
    test
    our
    iterator
    


## 4. Regular expression
