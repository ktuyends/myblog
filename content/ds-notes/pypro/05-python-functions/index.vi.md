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

Cú pháp:

```python
# Áp dụng một hàm cho từng phần tử của iterable
map(func, iterable)

# Ví dụ 1
def fact(n):
    return 1 if n < 2 else n * fact(n-1)

# Hàm map trả về một đối tượng map
l = list(map(fact, [1, 2, 3, 4, 5]))
```

```python
# Ví dụ 2, kết hợp map với lambda
l1 = [1, 2, 3, 4, 5]
l2 = [10, 20, 30, 40, 50]
m = map(lambda x, y: x+y, l1, l2)
list(m)
```

### 3.2. Filter

Hàm `filter()` sẽ áp dụng một hàm lọc (hàm trả về `True` hoặc `False`) cho từng phần tử của iterable, và trả về những phần tử thỏa mãn điều kiện lọc.

```python
# Cú pháp tương tự map
filter(func, iterable)

# Ví dụ
def is_even(n):
    return n % 2 == 0

# Lọc những giá trị chia hết cho 2
l = [1, 2, 3, 4, 5, 6, 7, 8, 9]
result = filter(is_even, l)
print(list(result))
```

### 3.3. Reduce

```python
# Hàm reduce 
# Cơ chế: reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
from functools import reduce
reduce(func, iterable)

# Ví dụ 1:
def my_add(a, b):
    result = a + b
    print(f"{a} + {b} = {result}")
    return result

numbers = [0, 1, 2, 3, 4]

reduce(my_add, numbers, 100)

# output
# 100 + 0 = 100
# 100 + 1 = 101
# 101 + 2 = 103
# 103 + 3 = 106
# 106 + 4 = 110
# 110
```

```python
# Ví dụ 2:
num1 = [15,12,30,4,5]
num2 = reduce(lambda x,y: x if x>y else y, num1)
print(num2)
```

{{< figure src="./python-reduce-2.png" width=75% >}}


## 4. Scopes

### 4.1. Scopes và Namespaces

Nhớ lại, khi một đối tượng được gán cho một biến, ví dụ `a = 100` thì biến đó trỏ đến một đối tượng nào đó và chúng ta nói rằng biến đó được liên kết với đối tượng đó. Khi đó, chúng ta có thể truy cấp đến đối tượng từ một số nơi trong đoạn code sử dụng tên biến nói trên.

Tuy nhiên, không phải chỗ nào trong đoạn code chúng ta cũng có thể truy cập đến đối tượng trên, nó chỉ tồn tại ở trong một phần hoặc phạm vi cụ thể của mã nguồn, phần mã nguồn mà ở đó tên biến và đối tượng được xác định - còn được gọi là **lexical scope** của các biến. Các tên này sẽ được lưu trữ trong Namespaces và mỗi Scope sẽ có một Namespaces riêng.

{{< figure src="./scopes.png" width=60% >}}

### 4.2. Global Scope

Global scope về cơ bản là chỉ các đối tượng được khai báo trong phạm vi module hay nói cách khác là nằm trong một file duy nhất. Các biến built-in và global có thể được sử dụng bất kỳ đâu trong module kể cả trong các hàm.

Nếu chúng ta tham chiếu đến một tên biến trong một scope và Python không tìm thấy nó trong namespace của scope đó, nó sẽ tìm kiếm trong không gian tên của enclosing scope (scope gần nhất chứa scope hiện tại), cứ như thế cho thấy khi tìm thấy thì dừng lại.

### 4.3. Local Scope

Khi chúng ta tạo một hàm, chúng ta có thể tạo ra các biến bên trong hàm đó. Các biến được tạo ra bên trong một hàm sẽ không được tạo cho đến khi hàm được gọi.

Ví dụ chúng ta có một hàm như sau trong một module nào đó:

```python
def func1(a, b):
    # do something
    pass
```

Khi module được gọi, hàm func1 sẽ nằm trong không gian tên của module (global scope) nhưng mọi thứ bên trong hàm chưa được tạo cho đến khi hàm được gọi. Mỗi khi chúng ta gọi hàm thì một scope mới sẽ được tạo ra và các biến được xác định bên trong hàm đó sẽ được gán cho scope đó - **local scope**.

```python
# Ví dụ 2
a = 10 # a thuộc global scope

def myFunc(b):
    print(True) # print và True thuộc built-in scope
    print(a) # a thuộc global scope
    print(b) # b thuộc local scope

myFunc(300) # một local scope mới được tạo, b trỏ đến đối tượng lưu trữ 300
myFunc('a') # thêm một local scope nữa được tạo, b trỏ đến đối tượng lưu trữ 'a'
```

### 4.4. Global keyword

Khi chúng ta truy xuất một giá trị của một biến bên trong một hàm. Python sẽ tìm kiếm nó theo thứ tự: _Local -> Nonlocal -> Global -> Built-in_. Do đó, khi chúng ta sửa giá trị của một biến global bên trong một hàm, biến global sẽ không thay đổi. Để thực hiện sửa đổi biến global ta phải khai báo nó bằng từ khóa `global`:

```python
a = 0
def myFunc():
    global a # Khai báo biến global
    a = 100
    print(a)
myFunc() ## 100
print(a) ## 100
```

```python
a = 10
def func1():
    print(a) ## a chỉ được tham chiếu đến trong function chứ không được gán -> tại compile-time, a là non-local

def func2():
    a = 100 ## a được gán trong function -> tại compile-time, a là local

def func3():
    global a
    a = 100 ## a được gán và được chỉ định global -> tại compile-time, a là global

def func4():
    print(a)
    a = 100 # tại compile-time, a là local

# khi gọi hàm func4()
# print(a) sẽ dẫn đến một run-time error bởi vì a là local,
# và chúng ta đang tham chiếu đến nó trước khi chúng ta gán một
# giá trị cho nó.
func4()
```

### 4.5. Inner functions

Giả sử ta có một hàm như sau:

```python
# global scope
x = 0

def outer():
    # Enclosing scope
    x = 10

    def inner():
        # Local scope
        x = 12
```

Với những hàm lồng nhau như thế này, có một số đặc điểm:

- Cả hai hàm `outer()` và `inner()` đều có quyền truy cập vào global scope và built-in scope.
- Hàm `inner()` có thể truy cập vào enclosing scope
- Một scope mà không phải là local, cũng không phải là global gọi là **nonlocal**.

Về cơ bản chúng ta không thể sửa giá trị của biến enclosing scope bên trong local scope. Nhưng nếu chúng ta vẫn muốn làm điều đó thì tương tự như global, ta phải khai báo biến `nonlocal` bên trong local scope.


## 5. Closures

Giả sử ta có ví dụ sau:

```python
# Hàm inner được định nghĩa bên trong hàm outer
# Hàm outer trả về giá trị là hàm inner
# x bên trong hàm inner được gọi là free variable
def outer():
    x = 1
    def inner():
        print(f'x in outer function: {x}')
    return inner
```

Khi chúng ta gọi hàm `outer()`, hàm `inner()` được trả về cùng với giá trị của biến `x = 1` được khởi tạo và ghi nhớ. Trong trường hợp này, hàm lồng nhau được gọi là closures. Hay nói một cách nôm na thì Closures là một hàm mà giá trị trả về là một hàm khác.

Ví dụ sử dụng closures thay thế hàm đệ quy:

Một dãy số Fibonacci là một chuỗi số, mà mọi số là tổng của hai số đứng trước nó (không tính 2 số đầu tiên), ví dụ như: 0, 1, 1, 2, 3, 5, 8, 13,...là một dãy Fibonacci. Hàm closue:


```python
# Hàm closure
def fib():
    x1 = 0
    x2 = 1
    def get_next_number():
        nonlocal x1, x2
        x3 = x1 + x2
        x1, x2 = x2, x3
        return x3
    return get_next_number
```

Bây giờ, ta muốn tính chuỗi Fibonacci gồm 15 số:


```python
fibonacci = fib()
for i in range(3, 17):
    num = fibonacci()
    print(f'The {i}th Fibonacci number is {num}')
```

    The 3th Fibonacci number is 1
    The 4th Fibonacci number is 2
    The 5th Fibonacci number is 3
    The 6th Fibonacci number is 5
    The 7th Fibonacci number is 8
    The 8th Fibonacci number is 13
    The 9th Fibonacci number is 21
    The 10th Fibonacci number is 34
    The 11th Fibonacci number is 55
    The 12th Fibonacci number is 89
    The 13th Fibonacci number is 144
    The 14th Fibonacci number is 233
    The 15th Fibonacci number is 377
    The 16th Fibonacci number is 610
    

## 6. Decorators

{{< figure src="./decorator_tutorial_code.png" >}}

### 6.1. Decorators là gì

Decorators là một Pattern, trong đó một hàm (class) sẽ nhận tham số đầu vào là một hàm (class) và trả về kết quả là một hàm khác (class) khác. Hàm được trả về có thể được mở rộng hoặc sẽ có kết quả khác với hàm đầu vào.

Ví dụ, ta có một hàm tính tổng:


```python
# Hàm tính tổng các đầu vào
def add(*args):
	return sum(args)
```

Bây giờ ta sẽ viết một hàm, tính thời gian thực thi của hàm trên:


```python
import time

def log(func):
	def func_with_log(*args, **kwargs):
		start_at = time.time()
		ret = func(*args, **kwargs)
		print("Take", time.time() - start_at, "second")
		return ret
	return func_with_log
```


```python
# Cách sử dụng
# add = log(add)
@log
def add(*args):
	return f'This sum is {sum(args)}'

# Xem kết quả
add(1, 2, 12, 30)
```

    Take 0.0 second
    




    'This sum is 45'



### 6.2. Nested decorators

Một hàm có thể có nhiều Decorators hay không, câu trả lời là có nha. Thứ tự thực thi của các Decorators sẽ từ trong ra ngoài. Ví dụ:

```python
def decorator1(func):
	def new_func(*args, **kwargs):
		print('Decorator 1')
		return func(*args, **kwargs)
	return new_func

def decorator2(func):
	def new_func(*args, **kwargs):
		print('Decorator 2')
		return func(*args, **kwargs)
	return new_func

# Thứ tự: decorator1(decorator2(func))
@decorator1
@decorator2
def func(msg):
	print('Original func:', msg)
```

Với ví dụ này, đầu tiên `@decorator2` sẽ áp dụng với hàm `func` trước, sau đó `@decorator1` sẽ áp dụng với hàm `func` đã được sửa đổi.

### 6.3. Decorators có tham số

Decorators có tham số đơn giản là ta sử dụng một hàm mới gồm các tham số tùy chỉnh bao quanh hàm decorator hiện tại, ví dụ:

```python
# decorator có tham số
import time
def log(show_input = False):
	def config(func):
		def func_with_log(*args, **kwargs):
			start_at = time.time()
			ret = func(*args, **kwargs)
			print(func.__name__, "takes", time.time() - start_at, "second")
			if show_input:
				print("Input:", args, kwargs)
			return ret
		return func_with_log
	return config

# Sử dụng
@log(show_input = True)
def need_log_input():
	# Do something

@log(show_input = False)
def dont_need_log_input():
	# do something
```

### 6.4. Tham số tùy chọn

Trong một số trường hợp, các bạn sẽ thấy cùng một Decorator, nhưng có chỗ thì sử dụng tham số, có chỗ thì không. Chúng ta thử phân tích ví dụ này:

```python
def log(func = None, show_input = None):
	if func is None:	# lúc gọi @log(show_input=True)
		return lambda origin_func: log(origin_func, show_input=show_input)

	if show_input is None:
		show_input = False 	# giá trị mặc định

	def func_with_log(*args, **kwargs):
		start_at = time.time()
		ret = func(*args, **kwargs)
		print(func.__name__, "takes", time.time()-start_at, "second")
		if show_input:
			print("Input:", args, kwargs)
		return ret
	return func_with_log
```

**Trường hợp 1: Khi chúng ta sử dụng `@log` mà không kèm tham số**

```python
@log
def old_func():
    # Do something
```

Khi chúng ta chạy chương trình trên, cú pháp sẽ tương đương với: 

`new_func = log(old_func, show_input = None)`

Và chương trình sẽ bỏ qua phần này:

```python
if func is None:	# lúc gọi @log(show_input=True)
	return lambda origin_func: log(origin_func, show_input = show_input)
```

Bây giờ nó đã giống với các Decorators phía trên của chúng ta.

**Trường hợp 2: Khi chúng ta sử dụng `@log(show_input = True)`**

```python
@log(show_input = True)
def old_func():
    # Do something
```

Khi này, cú pháp sẽ tương đương với: `new_func = log(show_input = True)(old_func)`, nghĩa là chương trình gọi lại hàm đệ quy `log()` một lần nữa với các tham số mới là `old_func` và `show_input = True`. Ôi thật là rắc rối và khó hiểu!


