---
title: "Pypro - Cấu trúc điều khiển"
subtitle: ""
slug: python-flow-control
date: 2021-12-26
lastmod: 2021-12-26
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
series: [Python Programming]
series_weight: 6
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
## 1. Mệnh đề *if...else*

Câu lệnh đơn giản:

```python
my_var = 10

# check if my_var is 20, else print something else, notice the indentations
if my_var == 20:
  print('Yes its 20')
else:
  print('Its something else')
```

Mở rộng câu lệnh với nhiều điều kiện:

```python
my_var = 30

# same example with different value
if my_var == 20:
  print('Yes its 20')
elif my_var == 30:
  print('Yes its 30')
else:
  print('Its something else')
```

Cú pháp lồng nhau:

```python
my_value = 18

# notice the indentation here
if my_value > 10:
  if my_value < 20:
    print("my_value is between 10 and 20")
  else:
    print("my_value is greater than 20")
else:
  print("my_value is smaller than 10")
```

Cú pháp rút gọn:

```python
## Ternary Operator: SYNTAX => [on_true] if [expression] else [on_false] 
my_var = "Yes" if 20%2 == 0 else "No"
# here is 'Yes' is the output when 'if' condition is satisfied, else 'No' is the output
print(my_var) # "Yes"
```

True và False:

```python
# Truthy(True values): non-zero numbers(including negative numbers),True,Non-empty Data-structures/sequences
# Falsy(False values): 0,0.0,0j,None,False,[],{},(),"",range(0)

my_var = 10
my_var1 = None

## Some Examples
# my_var is a non-zero number, which is Truthy, so 'if' will execute
if my_var: 
  print("printed") # printed

# my_var1 is 'None', which is Falsy, so 'if' will not execute  
if my_var1: 
  print("not printed")

# check a empty tuple
if ():
  print("not printed")

# check a non-empty list
if [23,45,34]:
  print("printed")

# By default user-defined object is also Truthy, you can manipulate using '__bool__()' special method
# can also use 'bool()' built-in function to check the Truth value  
print(bool(42)) # True
print(bool("This?")) # True
print(bool("")) # False
print(bool(None)) # False
# Explore the rest!
```



## 2. Mệnh đề for

```python
my_list = [10,20,30,40,50]

## regular looping using range object
for i in range(len(my_list)): # [0:4]
  print(my_list[i])

## pythonic loops
for v in my_list:
  print(v)
# or 
for a in [10,20,30,40,50]:
  print(a)   
  
## there's also a 'else' condition, when a "for" loop is not executed
# if no statement has executed inside a "for" loop, this 'else' condition will execute
# if break, else not executed
for v in []:
  print("List has no elements")
else:
  print("So this will execute")
```



## 3. Mệnh đề while

```python
i=0
my_list = [10,20,30,40,50]

# define a while loop, till i is smaller than length of my_list
while i < len(my_list):
  print(my_list[i])
  i+=1 # similar to 'i=i+1', since 'i++' is not supported
  
# infinite looping
while True:
  # do something
  # but remember to stop at some point!
```

## 4. break và continue

- break: thoát khỏi vòng lặp
- continue: bỏ qua phần còn lại của lần lặp hiện tại, bước vào lần lặp tiếp theo

```python
i=-1
my_list = [10,20,30,40,50]

while i<len(my_list):
  i+=1
  if i == 0:
    continue
  if i == 4:
    break
  print(my_list[i]) # [20,30,40]
```
