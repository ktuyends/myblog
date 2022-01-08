---
title: "Pypro - Xử lý ngoại lệ"
subtitle: ""
slug: python-exception-handling
date: 2021-12-27
lastmod: 2021-12-27
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
series: [Python Programming]
series_weight: 7
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
## 1. Các loại lỗi trong Python

{{< figure src="exception.png" >}}

### 1.1. Lỗi biên dịch

Lỗi này thường do cú pháp không chính xác *(SyntaxError)* hoặc thụt lề *(SyntaxError)*

```python
## Example 1: wrong indentation in condition
a = 30
if a == 30:
    print("Execute this")
     print("This will raise a Indentation error") # IndentationError

## Example 2: missing closing brackets in list and string  
data = [232,54,65 # SyntaxError
data = "this string is not complete # SyntaxError

## Example 3: missing colon in function 
def myfun() # SyntaxError
    print("my function")
```

### 1.2. Lỗi thực thi 

Đây là lỗi phát sinh trong quá trình thực thi chương trình. Ví dụ lỗi chia cho số `0`.

```python
## Example 1: indexing error
a = [34,56,32,87]
print(a[6]) # IndexError

## Example 2: dividing by zero
print(34/0) # ZeroDivisionError

## Example 3: accessing unknown attribute 
import math
math.square # AttributeError

## Example 4: raise a warning
import warnings
warnings.warn("Something is not right.")
print("This can execute")
```

### 1.3. Lỗi Logic

Đây là lỗi mà chương trình vẫn thực thi bình thường, nhưng kết quả trả về lại không phải kết quả chúng ta mong đợi

```python
## Example 1: accessing wrong index
my_list = [82,92,38,42,54,23,64,87]

# printing last 3 values
print(my_list[-2:]) # [64, 87]

# here program has no error, but instead of printing 3
# its only printing 2 numbers, because we provided wrong index
# this example is not hard to fix, but in larger programs it consumes a lot of 
# time to find which object/variable/function must have caused the wrong output 
```

### 1.4. Lỗi đánh giá

Đây là một loại lỗi liên quan đến việc giá trị của một biểu thức không đạt yêu cầu.

Ví dụ, bạn yêu cầu nhập vào một số chẵn, nếu người dùng nhập vào một số lẻ thì đây có thể xem như là lỗi đánh giá *(assert error)*.


## 2. Xử lý lỗi

Về cơ bản, khi gặp phải lỗi Python sẽ dừng thực hiện chương trình và đưa ra thông tin về lỗi mà chương trình gặp phải.

Trong Python, ứng với mỗi loại lỗi, sẽ có một class riêng. Ví dụ, để mô tả lỗi chia cho số 0, Python sử dụng class *ZeroDivisionError*,...Ta có rất nhiều class như này, và chúng được gọi là những ngoại lệ được xây dựng sẵn *(built-in exception)*.

### 2.1. Cú pháp tổng quát

```python
try:
   # do something

except ValueError as vE:
   # handle ValueError exception

except (TypeError, ZeroDivisionError):
   # handle multiple exceptions
   # TypeError and ZeroDivisionError

except:
   # handle all other exceptions

else:
   # Nếu không thực thi except, sẽ thực thi else

finally:
   # luôn luôn thực thi
```

### 2.2. Từ khóa raise

`raise` được sử dụng để đưa ra một ngoại lệ bên trong chương trình. Nếu ta sử dụng `raise` bên trong câu lệnh `try-except` nó sẽ nhảy đến ngoại lệ được đưa ra.

```python
>>> raise KeyboardInterrupt
Traceback (most recent call last):
...
KeyboardInterrupt
```

```python
>>> raise MemoryError("This is an argument")
Traceback (most recent call last):
...
MemoryError: This is an argument
```

### 2.3. Từ khóa assert

Trong Python, `assert` chỉ đơn giản là kiểm tra một biểu thức logic. Nếu nó trả về `True`, assert không làm gì hết và chuyển đến câu lệnh tiếp theo. Nếu nó trả về `False`, assert dừng chương trình và đưa ra thông báo lỗi.

Cú pháp:

```python
assert <condition>
assert <condition>,<error message>
```


## 3. Xây dựng ngoại lệ

Để xây dựng một ngoại lệ, ta tạo một class kế thừa thì class `Exceptions`:


```python
# Tạo một class kế thừa từ class Exception
class CustomError(Exception):
    pass

# Raise
raise CustomError

```


    ---------------------------------------------------------------------------

    CustomError                               Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_12416/509278271.py in <module>
          4 
          5 # Raise
    ----> 6 raise CustomError
    

    CustomError: 



```python
raise CustomError("An error occurred")
```


    ---------------------------------------------------------------------------

    CustomError                               Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_12416/4012702173.py in <module>
    ----> 1 raise CustomError("An error occurred")
    

    CustomError: An error occurred


**Ví dụ 1: tạo một ngoại lệ đơn giản**



```python
# define Python user-defined exceptions
class Error(Exception):
    """Base class for other exceptions"""
    pass

class ValueTooSmallError(Error):
    """Raised when the input value is too small"""
    pass

class ValueTooLargeError(Error):
    """Raised when the input value is too large"""
    pass
```


```python
# you need to guess this number
number = 10

# user guesses a number until he/she gets it right
while True:
    try:
        i_num = int(input("Enter a number: "))
        if i_num < number:
            raise ValueTooSmallError
        elif i_num > number:
            raise ValueTooLargeError
        break
    except ValueTooSmallError:
        print("This value is too small, try again!")
        print()
    except ValueTooLargeError:
        print("This value is too large, try again!")
        print()

print("Congratulations! You guessed it correctly.")
```

**Ví dụ 2: Tạo một ngoại lệ nâng cao hơn**


```python
class SalaryNotInRangeError(Exception):
    """Exception raised for errors in the input salary.

    Attributes:
        salary -- input salary which caused the error
        message -- explanation of the error
    """

    def __init__(self, salary, message="Salary is not in (5000, 15000) range"):
        self.salary = salary
        self.message = message
        super().__init__(self.message)

    def __str__(self):
        return f'{self.salary} -> {self.message}'


salary = int(input("Enter salary amount: "))
if not 5000 < salary < 15000:
    raise SalaryNotInRangeError(salary)
```
