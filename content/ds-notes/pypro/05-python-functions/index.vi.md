---
title: "Pypro - Functions"
subtitle: ""
slug: python-functions
date: 2022-03-03
lastmod: 2022-03-03
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
series: [Python Programming]
series_weight: 5
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
## 1. Functions

Functions (Hàm) là một khối code, có tổ chức, có thể tái sử dụng dưới một cái tên được định nghĩa để thực hiện một nhiệm vụ cụ thể nào đó. Hàm có thể có hoặc không có đối số, và sẽ trả về một giá trị.

### 1.1. Tạo hàm

```python
# Cú pháp
def function_name(parameter1, parameter2):
    """docstring"""
    # function body    
    # write some action
    return value1, value2
```

### 1.2. Tham số và đối số

Tham số (parameters) là tên xuất hiện khi chúng ta định nghĩa hàm.

```python
# name, age, skill là các tham số
def my_func(name, age, skill):
    pass
```

Đối số (arguments) là giá trị chúng ta truyền cho tham số khi gọi hàm:

{{< figure src="param-args.png" width=70% >}}

### 1.3. Đối số theo vị trí và theo keywords

Đối số theo vị trí là đối số được xác định dựa vào vị trí của tham số khi định nghĩa hàm. Còn đối số theo keywords là đối số xác định dựa vào tên tham số.

{{< figure src="args-types.png" width=70% >}}

### 1.4. Đối số *args và **kwargs

- `*args` đại diện cho các đối số theo vị trí, khi chúng ta không xác định được số lượng đối số sẽ truyền vào. `args` có thể thay thế bằng bất kỳ một tên nào khác, và nó là một tuple.
- `**kwargs` tương tự như `*args` nhưng nó đại diện cho các đối số theo keywords và nó là một dictionary.

Tổng quát khi định nghĩa hàm ta có:

{{< figure src="func.png" width=70% >}}


## 2. First class functions

### 2.1. Docstrings và annotations

Khi chúng ta sử dụng hàm `help()` trên một class, function, hoặc module,...Python sẽ đưa ra một số thông tin như:


```python
help(print)
```

    Help on built-in function print in module builtins:
    
    print(...)
        print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
        
        Prints the values to a stream, or to sys.stdout by default.
        Optional keyword arguments:
        file:  a file-like object (stream); defaults to the current sys.stdout.
        sep:   string inserted between values, default a space.
        end:   string appended after the last value, default a newline.
        flush: whether to forcibly flush the stream.
    
    

Để làm được như vậy, khi định nghĩa hàm, class,...ta sử dụng docstrings. Ví dụ:


```python
# Định nghĩa hàm
def fact(n):
    '''Calculates n! (factorial function)
    
    Inputs:
        n: non-negative integer
    Returns:
        the factorial of n
    '''
    
    if n < 0:
        '''Note that this is not part of the docstring!'''
        return 1
    else:
        return n * fact(n-1)

# Kết quả
help(fact)
```

    Help on function fact in module __main__:
    
    fact(n)
        Calculates n! (factorial function)
        
        Inputs:
            n: non-negative integer
        Returns:
            the factorial of n
    
    

Annotations là tính năng mới của Python, đưa ra các gợi ý về kiểu dữ liệu của các biến hoặc tham số của hàm, và kiểu dữ liệu trả về của một hàm. Cú pháp:

```python
# arg_type có thể là bất cứ thứ gì
# Nhưng thường là các kiểu dữ liệu như int, float, str, bool...
def func(arg: arg_type, optarg: arg_type = default) -> return_type:
    ...

# Ví dụ:
def my_func(num1: int, num2: int=10) -> int :
    return num1 + num2
```

### 2.2. Hàm ẩn danh (lambda)

Hàm ẩn danh là một hàm giống hàm Python bình thường, nhưng khác biệt là chúng ta có thể định nghĩa mà không cần tên hàm và chỉ được định nghĩa trên một dòng. 

Cú pháp:

```python
# arguments: đối số
# expression: kết quả trả về
lambda arguments: expression
```

Ví dụ:

```python
# Hàm square
squares = lambda x: x*x

# Gọi hàm
print('Using lambda: ', squares(5))
```

{{< admonition type=notes title="Lưu ý" open=true >}}
Một số lưu ý khi định nghĩa hàm ẩn danh:

- Hàm ẩn danh không thể chứa các câu lệnh như `return, raise, pass...`
- Hàm ẩn danh chỉ chứa một biểu thức duy nhất.
- Hàm ẩn danh có thể được gọi trực tiếp mà không cần tên biến như ví dụ trên.

{{< /admonition >}}

Một số ví dụ khác với hàm ẩn danh:

```python
# Positional arguments
add = lambda x, y, z: x + y + z
print(add(2, 3, 4))
# Prints 9

# Keyword arguments
add = lambda x, y, z: x + y + z
print(add(2, z = 3, y = 4))
# Prints 9

# Default arguments
add = lambda x, y = 3, z = 4: x + y + z
print(add(2))
# Prints 9

# *args
add = lambda *args: sum(args)
print(add(2, 3, 4))
# Prints 9

# **args
add = lambda **kwargs: sum(kwargs.values())
print(add(x = 2, y = 3, z = 4))
# Prints 9
```


## 3. Higher-order functions

Một hàm nhận một hàm khác làm đối số, hoặc trả về một hàm được gọi là _higher-order functions_.

### 3.1. Map

### 3.2. Filter

### 3.3. Reduce

### 3.4. Partial functions



## 4. Scopes

### 4.1. Global

### 4.2. Local

### 4.3. Nonlocal

## 5. Closures

## 6. Decorators

