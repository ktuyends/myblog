---
title: "Pypro - Cấu trúc dữ liệu"
subtitle: ""
slug: python-structures
date: 2021-12-25
lastmod: 2021-12-25
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
## 1. List

List trong Python:

- Là một tập hợp các phần tử có thứ tự
- Các phần tử có thể có bất kỳ kiểu dữ liệu nào
- Thuộc nhóm Mutable, vì vậy ta có thể thực hiện các thao tác như thêm, sửa, xóa,...

### 1.1. Tạo một List

```python
# insert items inside '[]' brackets
my_list = [1,1,3,'a','cab boy',4.0]

# or create empty list
some_list = [] 

# or using the list() function
some_list = list()
```

### 1.2. Một số toán tử với list

```python
my_list = [23,65,12,76,10]

## Adding/Appending: adding values to list
my_var = 1
my_list.append(my_var)
print(my_list) # [23, 65, 12, 76, 10, 1]

## Altering: change values of list items
my_list[0] = 100
my_list[4] = 200
print(my_list) # [100, 65, 12, 76, 200]
```

```python
## Removing: remove first value from list
my_list.remove(my_var)

# remove using 'del' statement is mostly preferred, eg 'del my_list[index]'
del my_list[0] # or even with slicing, eg del my_list[2:4]

# or using 'pop' method of list, 'my_list.pop(index)'
# Note: del statement can be used to delete any other object too.
print(my_list) # [65, 12, 76, 200]

## Checking if some value is present in list
if 20 in my_list: # similar to "if some_var in my_list:" where "some_var = 20"
  print('not printed')
if 200 in my_list:
  print('printed')
```

### 1.3. Toán tử nối và lặp

```python
## Joining: join two or more lists
# using '+' operator
my_list1 = [2,4,5,6] + [34,7,4,2]
print(my_list1) # [2, 4, 5, 6, 34, 7, 4, 2]

# using 'extend()' method
my_list1.extend([3,6,2])
print(my_list1) # [2, 4, 5, 6, 34, 7, 4, 2, 3, 6, 2]

## Multiplying: using '*' operator on a list
eg_list = ['This',30]
print(eg_list*3) # ['This', 30, 'This', 30, 'This', 30]
```

### 1.4. Indexing, iterating và Slicing

```python
my_list = [1,1,3,'a','cab boy',4.0]
my_list1 = [45,23,5,6,34,6,22]

## Indexing: for accessing/altering elements
var_1 = my_list1[0] # as usual 0 is the first element
var_2 = my_list1[1]
print(var_1, var_2) # 45, 23

# altering values in list
my_list1[0] = 100
my_list1[1] = 200
print(my_list1) # [100, 200, 5, 6, 34, 6, 200] 

# checking if some value is present in list
if 20 in my_list1: # similar to "if some_var in my_list1:" where "some_var = 20"
  print('not printed')
if 200 in my_list1:
  print('printed')
```

```python
## Iterating: going over item by item from a list
for var in my_list1:
  print(var) # [2, 4, 5, 6, 34, 7, 4, 2, 3, 6, 2]
```

```python
## Slicing: for creating sub-list, syntax is [start_index:end_index:step]
print(my_list[3:5]) # ['cab', 1.0]
print(my_list[5:]) # [2.0, 1]
print(my_list[:3]) # [3, 'a', 'this way']
print(my_list[:5:2]) # [3, 'this way', 1.0]

# negative indexing similar to string
print(my_list[:-4]) # [3, 'a', 'this way']

# reverse a list
print(my_list[::-1]) # [1, 2.0, 1.0, 'cab', 'this way', 'a', 3]
```

### 1.5. List Comprehension

```python
## List comprehension: create a new list in a single line 
# Note: range function returns sequence of integers, we'll learn more on range later 
my_list1 = [x for x in range(10)]

# this is similar to 
my_list1 = []
for x in range(10):
    my_list1.append(x)

# comprehensions are syntactic sugar, they save lines of code
my_list2 = [[y for y in range(x)] for x in range(5)] # it can be nested
my_list3 = [abc for abc in range(10) if abc > 5] # if condition
my_list4 = [True if z > 5 else False for z in range(10)] # if with else condition
# Notice: the syntax difference between if and if..else clauses
# also try printing each of the list
```

### 1.6. Copy một list

```python
my_list = [1,2,3,4,5,6]
new_copy = my_list
del new_copy[0] # deleting first item

print(my_list, new_copy) # [2, 3, 4, 5, 6] [2, 3, 4, 5, 6]
# the deletion is reflected to of the lists because they refer to same object
# this behaviour is exclusive to mutable objects, the catch from 'Multiple Target assignment'
# modified mutable objects reflect changes to its references

## Creating a copy 
new_copy = my_list[:] # or "my_list.copy()"
del new_copy[0]
# now they do not refer to the same object 
print(my_list, new_copy) # [2, 3, 4, 5, 6] [3, 4, 5, 6]
```

### 1.7. Một số phương thức của list

```python
my_list1 = [10,50,40,50,60,80,15]
# reverses a list, its inplace so does not return anything

my_list1.reverse() 
print(my_list1) # [15, 80, 60, 50, 40, 50, 10]

# sorts a list, inplace
my_list1.sort()
print(my_list1) # [10, 15, 40, 50, 50, 60, 80]

# returns index of first arrival of given value 
print(my_list1.index(50)) # 3

# removes value from a list given value
my_list1.remove(15) 

# removes value from a list given index, also returns the value
print(my_list1.pop(5)) # 80

my_list1.clear() # list becomes empty
print(my_list1) # []
```

### 1.8. Một số hàm

```python
my_list1 = [10,50,40,50,60,80,15]

# returns sorted list of items in ascending order by default, 
# sorting is O(nLogn), for reversing pass 'reverse=True'
print(sorted(my_list1)) # [10, 15, 40, 50, 50, 60, 80]

# return length of list
print(len(my_list1)) # 7

# sum of variables
print(sum(my_list1)) # 305
print(sum([10, 20])) # 30
```

### 1.9. Chuyển đổi

```python
my_list = list((1,2,3,4,5)) # tuple to list
my_list = list({1,2,3,4,5}) # set to list
```

## 2. Tuple

Tuple tương tự như List, nhưng có một vài điểm khác:

- Tuple thuộc nhóm Immutable, vì vậy chúng ta không thể thay đổi, sửa, xóa các phần tử
- Tuple có thể sử dụng indexing, slicing và iterating nhưng không có Tuple Comprehension

### 2.1. Tạo tuple

```python
# insert items inside '()' brackets
my_tuple = (1,2,3,'we','are','one',5.0)

# create empty tuple
some_tuple = () # or using tuple() function

# Tuple một phần tử (values, )
one_tuple = (10, )
```

### 2.2. Một số toán tử

```python
## tuple is immutable, there is no append()/remove(), can't use 'del' like in list
# so to add a element join two tuples, and assign it to the previous/new variable
my_tuple = (1,2,3,4)
my_tuple += (5,) # adding another element as tuple, its basically joining two tuples
print(my_tuple) # (1, 2, 3, 4, 5)

# Notice: The target tuple should have ',' if single element is being added
some_tuple = (5) # this will give the type of variable inside parenthesis and not tuple, here 'int'
print(type(some_tuple)) # <class 'int'>
```

```python
## Joining: join two or more tuples
my_tuple1 = (34,65,23) + (34,34)
print(my_tuple1) # (34, 65, 23, 34, 34)

## Multiplying: using '*' operator on a tuple
my_tuple1 = (34,65,23) * 2
print(my_tuple1) # (34, 65, 23, 34, 65, 23)
```

### 2.3. Indexing, iterating và slicing

```python
my_tuple = (1,2,3,'we','are','one',5.0)

## Indexing: accessing item/character from tuple
my_var = my_tuple[0] # okay
my_tuple[0] = 23 # not okay because Immutable, raises TypeError
```

```python
## Iterating: going over item by item from a tuple
 for var in my_tuple:
   print(var) # (1,2,3,'we','are','one',5.0)

# checking if some value is present using the 'in' operator
if 5.0 in my_tuple:
  print('printed')
```

```python
## Slicing: for creating sub-tuple, syntax is [start_index:end_index:step] 
print(my_tuple[3:5]) # ('we','are')
print(my_tuple[5:]) # ('one',5.0)
print(my_tuple[:3]) # (1,2,3)
print(my_tuple[:5:2]) # (1,3,'are')

# negative indexing
print(my_tuple[:-4]) # (1,2,3) 
print(my_tuple[:-2:2]) # (1, 3, 'are')

# reverse a tuple
print(my_tuple[::-1]) # (5.0, 'one', 'are', 'we', 3, 2, 1)
```

### 2.4. Unpacking

```python
## unpacking tuple (more on unpacking later on)
a,b,c = (1,2,3) # unpacking values into a,b,c

# even below line does the same, 1,2,3 becomes a tuple and then unpacks into a,b,c 
# same is true when returning comma separated values from a function 
a,b,c = 1,2,3 # same as (1,2,3)

# this behaviour further aids in swapping without using extra variable,
# you can also do the same with more variables
a,b = b,a 
```

### 2.5. Một số phương thức

```python
my_tuple1 = (3,2,6,2,5,3,1,1)

# Returns number of occurrences of value.
print(my_tuple1.count(3)) # 2

# Returns the first index of value.
print(my_tuple1.index(2)) # 1
```

### 2.6. Một số hàm

```python
my_tuple = (3,6,1,8,2,3)

# returns sorted list of items in ascending order by default
# can be reversed using the reverse parameter
print(sorted(my_tuple, reverse=True)) # [8, 6, 3, 3, 2, 1]

# returns length of tuple
print(len(my_tuple)) # 6
```

### 2.7. Chuyển đổi

```python
my_tuple = tuple([1,2,3,4,5]) # list to tuple
my_tuple = tuple({1,2,3,4,5}) # set to tuple
```

### 2.8. NamedTuple

NameTuple hiểu đơn giản, là một mở rộng của tuple cho phép chúng ta truy cập vào các phần tử dựa vào tên thay vì vị trí. 

**Tạo Numedtuple**

```python
from collections import namedtuple
import sys

# first parameter of namedtuple is typename: string which is name of tuple subclass
# second parameter is field_names: iterable/string  which has names of fields/variables/data tuple will contain 
Name_tup = namedtuple("mynamedtuple", ['a', 'b'])
# or provide names from a single string (separated by space)
Name_tup = namedtuple("mynamedtuple", "a b")

# print the class name 
print(Name_tup) # <class '__main__.mynamedtuple'>
```

```python
# create the namedtuple object
name_tup1 = Name_tup(42,65)

# can also create another object with different data type
name_tup2 = Name_tup("oh","this")

print(name_tup1) # mynamedtuple(a=42, b=65)
print(name_tup2) # mynamedtuple(a='oh', b='this')

# accessing elements with names
print(name_tup2.a) # oh
print(name_tup2.b) # this
```

```python
# comparing with regular tuple
print(name_tup1 == (42, 65)) # True

# comparing their sizes
print(sys.getsizeof(name_tup1), sys.getsizeof((42, 65))) # 56, 56

# like regular tuple immutable
name_tup1[0] = 32 # TypeError
```

**Indexing, iterating và slicing**

```python
from collections import namedtuple

Name_tup = namedtuple("mynamedtuple", ['aa', 'bbk', 'cab'])
name_tup1 = Name_tup(42,60,52)

## Indexing like tuples
print(name_tup1[0]) # 42
print(name_tup1[1]) # 60

## Iterating
for a in name_tup1:
    print(a) # 42,60,52

## Slicing
print(name_tup1[1:]) # (60, 52)
```

**Một số phương thức**

```python
from collections import namedtuple

Name_tup = namedtuple("mynamedtuple", ['aa', 'bbk', 'cab'])
name_tup1 = Name_tup(42,60,52)

# convert to dictionary
print(name_tup1._asdict()) # {'aa': 42, 'bbk': 60, 'cab': 52}

# replace the value, creates and returns a new mynamedtuple instance
print(name_tup1._replace(aa=32)) # mynamedtuple(aa=32, bbk=60, cab=52)
```

## 3. Dictionary

Dictionary trong Python:

- Là một tập hợp các phần tử có dạng *key:value*
- Thuộc nhóm Mutable nên chúng ta có thể thêm, sửa, xóa
- Các phần tử không có thứ tự, vì vậy chúng ta không thể thực hiện indexing, slicing
- Các keys trong Dictionary là immutable

### 3.1. Tạo dictionary

```python
# insert keys & values inside '{}' brackets
# Note: key & value are separated with ':' colon. i.e key:value

my_dict = {'e':23, 'w':65, 'q':52}

# create empty dictionary
my_dict = {} # or using dict() function
```

### 3.2. Một số toán tử

```python
my_dict = {'raf': 23, 'soe': 65, 'qr': 52, 10: 20}

## add operation
my_var = 20
key = 10
tuple_key = (20,)

# add item at key
my_dict[key] = my_var # adding 10: 20
my_dict[tuple_key] = 45 # adding (20,): 45
my_dict['az'] = 42 # adding 'az': 42
print(my_dict) # {'raf': 23, 'soe': 65, 'qr': 52, 10: 20, (20,): 45, 'az': 42}

## remove
del my_dict[tuple_key] # remove the item

## accessing element
key = 'qr'
my_var = my_dict[key] # can raise KeyError if not present

# use get() method to avoid KeyError, None is default, can be set to anything else
print(my_dict.get("ar", None)) # None

## check if key is inside my_dict   
if 'az' in my_dict:
  print('printed')
```

```python
my_dict = {'a':34, 'b': 42}
my_dict1 = {'z':5, 'y':3, 'x':4}

## Joining: join two dictionary, '+' operator is not supported
# using the update method of dictionary
my_dict.update(my_dict1)
print(my_dict) # {'a': 34, 'b': 42, 'z': 5, 'y': 3, 'x': 4}

# or use "my_dict | my_dict1" 
print(my_dict | my_dict1) # {'a': 34, 'b': 42, 'z': 5, 'y': 3, 'x': 4}

# or unpack them in a new dict 
print({**my_dict, **my_dict1}) # {'a': 34, 'b': 42, 'z': 5, 'y': 3, 'x': 4}
```

### 3.3. Iterating

```python
## Iterating: going over item by item from a dictionary
# use the items method for both keys, values unpacking
for k,v in my_dict1.items(): 
   print(k, v) # {'z':5, 'y':3, 'x':4}
```

### 3.4. Dictionary comprehension

```python
my_dict = {x:x*x for x in range(5)} # generating keys and values on the go
print(my_dict) # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# another way is using the zip function
my_keys = ['a', 'b', 'c']
my_values = [1,2,3]
my_dict = {k:v for k,v in zip(my_keys, my_values)}
print(my_dict) # {'a': 1, 'b': 2, 'c': 3}

# similar to list's comprehension, dictionaries also support if..else clause inside comprehension
# create a dictionary without a key 'a' 
my_dict = {k:v for k,v in zip(my_keys, my_values) if k is not 'a' }
```

### 3.5. Một số phương thức

```python
my_dict1 = {'a':1, 'b':2, 'c':3}
my_dict2 = {'z':50, 'y':40, 'x':30}

# returns a dict_keys object, it contains dictionary's keys, it is iterable, you can also convert it to list
print(my_dict1.keys()) # dict_keys(['a', 'b', 'c'])

# returns a dict_values object, it contains dictionary's values, it is iterable, you can also convert it to list
print(my_dict1.values()) # dict_values([1, 2, 3])

# returns a dict_items object, has keys & values, you know the rest
print(my_dict1.items()) # dict_items([('a', 1), ('b', 2), ('c', 3)])

# removes item(key,value) given key, which is 'a' here and returns value
print(my_dict1.pop("a")) # 1 
my_dict1.clear() # removes all items of dictionary
```

### 3.6. Chuyển đổi

```python
keys = [1,2]
values = [2,3]

my_dict = dict([keys, values]) # list to dictionary
my_dict = dict(((1,2), (2,3))) # tuple to dictionary
```

## 4. Set

Set trong Python:

- Là tập hợp các phần tử có dạng immutable, và không lặp lại
- Set có thể thực hiện các thao tác thay đổi, sửa xóa nhưng không có indexing và slicing

### 4.1. Tạo Set

```python
# insert values inside '{}' brackets
my_set = {9,1,5,2,20} # Notice: dictionary like parenthesis but without keys

# items order don't matter, so while printing order might differ
print(my_set) # {1, 2, 20, 5, 9}

# create a empty set
my_set = set() 
```

### 4.2. Các toán tử cơ bản

```python
my_var = 4
my_set = {9,1,5,2,20}

## add
my_set.add(my_var) # if repeated value, it will not be added again 

## remove
my_set.remove(my_var) # removes a member, raises KeyError if not found

## accessing element: indexing is not supported
my_set[0] # not allowed, TypeError: 'set' object is not subscriptable.

# so use in operator to check if my_var is inside my_set   
if my_var in my_set: 
  print('not printed')
```

```python
a = {54,23,67}
b = {34,65,55.6}

## Joining: join two sets, '+' operator is not supported, use the update method
a.update(b) 
print(a) # {65, 34, 67, 55.6, 54, 23}

## Iterating: going over item by item from a set
for x in a: 
   print(x) # {65, 34, 67, 55.6, 54, 23}
```

### 4.3. Set Comprehension

```python
# creating a set using comprehensions
my_set = {a for a in (10,10,20,30,60,20,40)}

# similar to previous comprehensions, there is also multiple comprehension
my_set = {(a,b) for a in range(2) for b in range(3)}

# Notice: (a,b) is a tuple inside a set
# above expression is similar to
my_set = set()
for a in range(2):
    for b in range(3):
        my_set.add((a, b))
print(my_set) # {(0, 1), (1, 2), (0, 0), (1, 1), (0, 2), (1, 0)}
# you can try practicing different combinations of comprehensions  
```

### 4.4. Một số phương thức

```python
my_set1 = {3,5,7,1,8}
my_set2 = {1,2,3,4,5}

# find intersection, or use 'my_set1 & my_set2'     
print(my_set1.intersection(my_set2)) # {1, 3, 5}

# to find union, or use 'my_set1 | my_set2'   
print(my_set1.union(my_set2)) # {1, 2, 3, 4, 5, 7, 8}

# find difference in my_set1 and my_set2
print(my_set1.difference(my_set2)) # {8,7}

# checks if my_set2 is a subset of my_set1
print(my_set1.issubset(my_set2)) # False

# checks if my_set2 is a superset of my_set1
print(my_set1.issuperset(my_set2)) # False

# removes all members of set
my_set2.clear() 

# create a copy of a set, a shallow copy
my_copy = my_set1.copy() 
# it means copying only references of original items into a new sequence, 
# so if a item isn't a literal constant like a list, 
# any modification made inside that list will be reflected to that item of a new copy 
```

### 4.5. Chuyển đổi

```python
my_list = [1,2,3,4,5]

# here my_list is mutable, but set() function unpacks the items from my_list
my_set = {my_list} # this raises TypeError
my_set = set(my_list) # this unpacks items from list to set

# also if my_list contained a list inside it, TypeError: unhashable type: 'list' is raised
my_set = set((1,2,3,4,5)) # tuple to set
```

### 4.6. Frozenset

Frozenset giống như Set, nhưng có một điểm khác nhau là Set thuộc nhóm Mutable, còn Frozenset thuộc nhóm Immutable.

**Tạo frozenset**

```python
# using a list
my_fset = frozenset([10,65,65,2,7,94,34,42,21])

# or any other iterable
my_fset = frozenset((10,65,65,2,7,94,34,42,21))
print(type(my_fset)) # <class 'frozenset'>
print(my_fset) # frozenset({65, 2, 34, 7, 10, 42, 21, 94})

## immutable 
my_fset.add(20) # AttributeError: 'frozenset' object has no attribute 'add'
my_fset.remove(20) # AttributeError: 'frozenset' object has no attribute 'remove'
```

**Một số phương thức**

```python
my_fset1 = frozenset({3,5,7,1,8})
my_fset2 = frozenset({1,2,3,4,5})

# intersection 
print(my_fset1.intersection(my_fset2)) # frozenset({1, 3, 5})

# union
print(my_fset1.union(my_fset2)) # frozenset({1, 2, 3, 4, 5, 7, 8})

# difference
print(my_fset1.difference(my_fset2)) # frozenset({8, 7})

# creates a copy of a set
my_copy = my_fset1.copy() 

# checks if my_fset2 is a subset of my_fset1
print(my_fset1.issubset(my_fset2)) # False

# checks if my_fset2 is a superset of my_fset1
print(my_fset1.issuperset(my_fset2)) # False
```

## 5. Stack và Queue

### 5.1. Stack (Ngăn xếp)

{{< figure src="stack.webp" >}}

Stack trong Python, hiểu một cách đơn giản nhất là ta có một danh sách. Sau đó, nếu chúng ta thêm một phần tử vào stack (push) nó sẽ được thêm vào cuối cùng của danh sách, ngược lại nếu chúng ta xóa một phần tử khỏi danh sách (pop) thì phần tử bị xóa là phần tử cuối cùng.

```python 
# Tạo một stack
stack_name = []

# add/remove operation
stack_name.append(item) # Thêm phần tử, push
stack_name.pop() # Xóa phần tử, pop
```

### 5.2. Queue (Hàng đợi)

{{< figure src="queue.webp" >}}

Trái ngược với stack, Queue có nguyên lý là FIFO - Nhập trước xuất trước.

```python
# create a queue
my_queue = []

## add/remove operation
my_queue.append(20) # enqueue: append at rear
my_queue.pop(0) # dequeue: remove at front
```

Sử dụng module *collections*

```python
from collections import deque

# create a deque using any iterable
my_list = [23,45,12,67,132,67]
dq = deque(my_list)

## Queue operations
dq.append(20) # # push: append at top
dq.popleft() # pop: remove at top
```

## 6. Numpy và Array

## 7. Pandas

## 8. Một số hàm làm việc với cấu trúc dữ liệu

### 8.1. Hàm Range

Cú pháp: `range(start_index=0, end_index, step=1) => range`

```python
# create a range object of length 20
my_range = range(20)
print(my_range) # range(0,20)
print(type(my_range)) # <class 'range'>

# create a range object values ranging 5 to 20
print(range(5,20)) # range(5,20)
# create a range object values ranging 6 to 20 with 2 steps
print(range(6,20,2)) # [6, 8, 10, 12, 14, 16, 18] 

## indexing a range
print(range(20)[0]) # 0
# supports slicing but its not preferred/recommended
print(range(20)[0:10]) 
# convert a range sequence to a list
print(list(range(5,10))) # [5,6,7,8,9] 

## looping a range object
for var in range(5): 
  print(var) # [1,2,3,4,5]

# reversing the order with step=-1 and end_index=-1
for var in range(5, -1, -1): 
  print(var) # [5,4,3,2,1]
```

### 8.2. Hàm enumerate

Cú pháp: `enumerate(iterable) => enumerate`

```python
# create a enumerate object from a list
my_list = [100,200,500,100]
print(type(enumerate(my_list))) # <class 'enumerate'>

# checking the item of enumerate, it is a tuple (index, value)
print(list(enumerate(my_list))[0]) # (0,100) 

# looping over the enumerate object
for i, val in enumerate(my_list):
  print(i) # 0,1,2,3
  print(val) # 100,200,500,100
```

### 8.3. Hàm zip

Cú pháp: `zip(*iterable) => zip`

```python
a = ['This','is','something']
b = (14, 3, 6)
c = {34,7} 
# create a zip object given a iterable
my_zip = zip(a)
print(type(zip(a))) # <class 'zip'>

# the length of zip is 2 because smallest is c and its length is 2
# so remaining values in a,c are ignored
print(len(list(zip(a, b, c)))) # 2
# convert to list in order to print
print(list(zip(a, b, c))) # [('This', 14, 7), ('is', 3, 34)]

# loop over the values
for v in zip(a, b, c):
  # v is a tuple with 3 values, so we can index them
  print(v[0], v[1], v[2]) # [('This', 14, 7), ('is', 3, 34)]
# or unpack them into named variables
for var1, var2 in zip(a,b):
  print(var1, var2) # [('This','is','something'), (14, 3, 6)]
```

### 8.4. Hàm sorted

Cú pháp: `sorted(iterable, key=None, reverse=False) => list`

```python
# sort a string
my_string = "ererer"
print(sorted(my_string)) # ['e', 'e', 'e', 'r', 'r', 'r']

# sort a tuple in reverse order
my_tuple = (14, 3, 6)
print(sorted(my_tuple, reverse=True)) # [14, 6, 3]

# sort a list by the length of sub-list
my_list = [[10,20,56,23,12],[200], [2,7,23]]

def my_fun(a):
  # return element you want iterable to be sorted by
  # here we are returning length of each element(sub-list)
  return len(a)

print(sorted(my_list, key=my_fun)) # [[200], [2, 7, 23], [10, 20, 56, 23, 12]]
# Notice: "my_fun" is passed and not called, we'll learn about this in the function's section.
```
