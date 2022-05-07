---
title: "Pypro - Lập trình hướng đối tượng"
subtitle: ""
slug: python-oop
date: 2022-03-04
lastmod: 2022-03-04
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
## 1. OOP là gì?

Lập trình hướng đối tượng, hiểu một cách nôm na là cách chúng ta tạo ra các đối tượng trong môi trường code trừu tượng hóa các đối tượng thực tế trong cuộc sống.

Các đối tượng _(Objects)_ có thể là con người, điện thoại, xe bus,...và điểm chung là chúng đều gồm có hai thành phần chính:

- Thuộc tính _(Attribute)_: Gồm những thông tin, đặc điểm của đối tượng.
- Phương thức _(Method)_: Gồm những hành được mà đối tượng có thể thực hiện được.

Ví dụ đối tượng Laptop có:

- Thuộc tính: màu sắc, kích thước, bộ nhớ, card màn hình,...
- Phương thức: tắt máy, bật máy, khởi động lại,...

Khi nhiều đối tượng có những đặc điểm như nhau, sẽ được gom lại thành một lớp các đối tượng _(Class)_. Và mỗi đối tượng trong lớp các đối tượng được gọi là _Instance_ (thực thể, một phiên bản cụ thể của class).

Ví dụ: lớp các đối tượng Laptop, sẽ có instance là laptop Asus, laptop Dell, laptop Thinkpad,...

## 2. Class

### 2.1. Tạo class đơn giản

Ví dụ tạo class Point:

```python
# Tạo class
class Point:
    # Bank class
    pass
```

Tiếp theo ta sẽ tạo một instance của class, tương tự như khi chúng ta gọi hàm:

```python
# Tạo instance của class Point
point_1 = Point()
```

### 2.2. Phương thức

Các bước tạo method tương tự như khi chúng ta tạo functions chỉ khác nhau là tham số đầu tiên của method luôn luôn là `self`, hiểu nôm na thì `self` là một đối tượng của class.

```python

class Point:
    """
    An abstract class to represnt a point on 2D Cartesian Plane
    """
    
    def give_info(self, x, y):
        """A function that gives info about this class"""
        print(f'This point is situated at ({x}, {y}) on 2D plane.')
```

Để sử dụng method, ta dùng cú pháp: `object.method()`

```python
# Tạo instance
obj1 = Point()

# Gọi phương thức
# This point is situated at (5, 10) on 2D plane.
obj1.give_info(5, 10)
```

Một ví dụ nữa, chúng ta sẽ tạo một phương thức đặt tọa độ cho đối tượng trong class Point và tính khoảng cách từ đối tượng đến gốc tọa độ:

```python
# Tạo class
class Point:
    
    def set_coords(self, x, y):
        """A function to set the coordinates of the point"""
        self.x = x
        self.y = y

    def distance_to_origin(self):
        """
        A method to calculate the distance between the point and the origin
        """
        return np.sqrt(self.x ** 2 + self.y ** 2)

# Kết quả
point_1 = Point()
point_1.set_coords(3, 4)
point_1.x # 3
point_1.y # 4
point_1.distance_to_origin() # 5
```

### 2.3. Thuộc tính

Cho tới nay, chúng ta đã biết cách gán thuộc tính cho một đối tượng sử dụng methods. Bây giờ ta giả sử một đối tượng có rất nhiều thuộc tính, và với mỗi thuộc tính ta lại tạo một method, như vậy code của chúng ta sẽ trở lên cồng kềnh và không cần thiết. Python có sẵn một phương thức khởi tạo `__init__()` cho phép ta tạo các thuộc tính khi xây dựng class.

```python
# Tạo class với thuộc tính
class Point:

    def __init__(self, x, y):
        self.x = x
        self.y = y

# Tạo instance
point = Point(4, 5)
point.x # 4
point.y # 5
```

## 3. Class và instance

### 3.1. Biến instance và class

Biến instance là biến chứa những thuộc tính đặc trưng cho một đối tượng và mỗi đối tượng có thể có giá trị khác nhau. Về cơ bản là khi chúng ta định nghĩa một thuộc tính bên trong `__init__()`, các biến được định nghĩa với từ khóa `self.var` được gọi là biến instance. 

Biến class _(class attribute)_ là một biến gắn liền với chính class, bên ngoài các phương thức, có thể được truy xuất từ các đối tượng và có giá trị chung cho tất cả các đối tượng. Chúng ta có thể trực tiếp truy cập vào biến class mà không cần khởi tạo đối tượng bằng cú pháp: `class_name.class_attribute`

Ví dụ:

```python
# wheels và car_type là biến class
# model, year là biến instance
class Car:

    wheels = 4
    car_type = "sports car"

    def __init__(self, model, year):
        self.model = model
        self.year = year

# Tạo instance
lambo = Car("Lamborghini", 2021)
bmw = Car("BMW", 2021)

# Giá trị khác nhau giữa các biến instance
lambo.model # Lamborghini
bmw.model # BMW

# Giá trị giống nhau giữa biến class
lambo.wheels # 4
bmw.wheels # 4
Car.wheels # 4
```

Một ví dụ của biến class trong Python:


```python
# import thư viện math
import math

# Biến pi, e,...
print(f'Số Pi: {math.pi}')
print(f'Số e: {math.e}')

```

    Số Pi: 3.141592653589793
    Số e: 2.718281828459045
    

Ví dụ làm việc với biến class:

```python
class Employee:
    
    min_salary = 30000
    min_age = 20
    
    def __init__(self, name, age, salary):
        self.name = name
        
        if age <= Employee.min_age:
            self.age = Employee.min_age
        else:
            self.age = age
        
        if salary <= Employee.min_salary:
            self.salary = Employee.min_salary
        else:
            self.salary = salary
```

**Lưu ý:** Nếu chúng ta sửa giá trị của biến class ở cấp độ instance, nghĩa là sử dụng từ khóa `obj.class_attribute` thì nó chỉ thay đổi giá trị của `obj` bị sửa chứ không thay đổi giá trị của các đối tượng khác. Nếu muốn sửa giá trị của biến class cho tất cả các đối tượng ta phải sử dụng `class_name.class_attribute`. 

### 3.2. Class và static method

Khi lập trình hướng đối tượng trong Python, chúng ta sẽ bắt gặp ba loại phương thức: instance, class và static method.

```python
class MyClass:
    def method(self):
        return 'instance method', self

    @classmethod
    def classmethod(cls):
        return 'class method', cls

    @staticmethod
    def staticmethod():
        return 'static method'
```

Phương thức đầu tiên là instance method, đây là phương thức chúng ta sẽ thường hay sử dụng nhất. Bạn có thể thấy phương thức này nhận vào đối số `self` làm tham số đầu tiên của phương thức. Nó trỏ đến các instance của class khi chúng được gọi. 

Phương thức thứ hai là class method, nó được bắt đầu bằng decorator `@classmethod` và nhận vào đối số `cls` làm tham số đầu tiên. Tham số `cls` là tham số trỏ trực tiếp đến class mà không phải là instance. Trong class method, chúng ta không được sử dụng `self`, nhưng có thể truy cập vào static method. Class method thường được sử dụng để tạo instance.

Phương thức cuối cùng là static method, hiểu một cách đơn giản thì nó giống một hàm bình thường có thể nhận vào số lượng tham số tùy ý nhưng không bao gồm `cls` và `self`. Do đó, nó không thể sửa đổi trạng thái của class và đối tượng.

Ví dụ:

```python
from datetime import date

class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def calculate_age(cls, name, birth_year):
        # calculate age an set it as a age
        # return new object
        return cls(name, date.today().year - birth_year)

    def show(self):
        print(self.name + "'s age is: " + str(self.age))

jessa = Student('Jessa', 20)
jessa.show()

# create new object using the factory method
joy = Student.calculate_age("Joy", 1995)
joy.show()
```

## 4. Inheritance

### 4.1. Kế thừa

Kế thừa trong lập trình hướng đối tượng nghĩa là khi một class kế thừa một class khác, nó sẽ sao chép tất cả các phương thức và thuộc tính từ class đó. Sau đó, nó có thể sử dụng các phương thức và thuộc tính có sẵn hoặc là sửa đổi lại để phù hợp với đối tượng mới. Cú pháp:

```python
class ChildClass(ParentClass):
    ## DO STUFF HERE
    ...
```

Class mà class hiện tại kế thừa được gọi là class cha hoặc class cơ sở, còn class hiện tại thì gọi là class con. Ví dụ:

```python

class Vehicle:
    def __init__(self, year, mpg, tank, mileage):
        self.year = year
        self.tank = tank
        self.mpg = mpg
        self.mileage = mileage

    def drive(self, n_miles):
        self.tank = self.tank - n_miles / self.mpg
        self.mileage += n_miles
        
        return self.tank, self.mileage

# Kế thừa
class Car(Vehicle):
    pass

# Tạo đối tượng
sedan = Car(2020, mpg=56, tank=10, mileage=1000)
```

Để kiểm tra xem một đối tượng, có phải là một instance của một class không ta sử dụng:

```python
isinstance(sedan, Vehicle) # True
isinstance(sedan, Car)     # True

simple_vehicle = Vehicle(2020, 60, 15, 1e7)
isinstance(simple_vehicle, Vehicle)  # True
isinstance(simple_vehicle, Car)      # False
```

### 4.2. Thêm thuộc tính

Chúng ta có thể thêm một số thuộc tính cho class con khi kế thừa:

```python
# Cách viết dài
class Car(Vehicle):
    def __init__(self, year, mpg, tank, mileage, model, color):
        self.year = year
        self.tank = tank
        self.mpg = mpg
        self.mileage = mileage

        # NEW ATTRIBUTES
        self.color = color
        self.model = model

# Cách viết ngắn gọn
class Car(Vehicle):
    def __init__(self, year, mpg, tank, mileage, model, color):

        # Iinitialize the attributes of the parent class
        Vehicle.__init__(self, year, mpg, tank, mileage)

        # NEW ATTRIBUTES
        self.color = color
        self.model = model

# Tạo instance
jaguar = Car(2015, 23, 10, 1000, 'Jaguar', 'black')
print(jaguar.year)
print(jaguar.mpg)
print(jaguar.model)
```

### 4.3. Thêm methods

```python
class Car(Vehicle):
    def __init__(self, year, mpg, tank, mileage, model, color):
        super().__init__(year, mpg, tank, mileage)
        self.color = color
        self.model = model
    
    def is_old(self):
        if self.year <= 2010:
            return True
        else: 
            return False
```

### 4.4. Sửa methods

```python
class Airplane(Vehicle):
    
    def __init__(self, mpg, tank, mileage, n_passengers):
        self.mpg = mpg
        self.tank = tank
        self.mileage = mileage
        self.n_passengers = n_passengers
    
    def fly(self, n_miles):
        # Sử dụng method drive từ Vehicle
        return Vehicle.drive(self, n_miles * self.n_passengers)


boeing = Airplane(51, 3500, 2e7, 200)
tank, mileage = boeing.fly(500)

print(f"Flew for 500 miles. "
      f"{round(tank, 2)} gallons remaining in tank.")
```

### 4.5. Một số lưu ý

Chúng ta sử dụng `super()` để đại diện cho class cha, khi đó ta không cần kèm theo từ khóa `self`.

Khi muốn ghi đè một hoặc một phần của một phương thức nào đó trong class cha, ta chỉ cần định nghĩa một phương thức mới trong class hiện tại với tên giống phương thức trong class cha.

## 5. Operator overloading 

### 5.1. Nạp chồng toán tử

Nạp chồng toán tử là cách chúng ta ghi đè hành vi của một số toán tử trong Python.

Ví dụ:


```python
# Toán tử cộng khi áp dụng với 2 số
10 + 4
```




    14




```python
# Toán tử + khi áp dụng với list
["list1"] + ["list2"]
```




    ['list1', 'list2']



Như chúng ta thấy, với mỗi đối tượng, hành vi của các toán tử có đôi khi không giống nhau. Mỗi toán tử trong Python sẽ đi kèm với một hàm đặc trưng nào đó. Để xem list các hàm đặc trưng mà một đối tượng hỗ trợ ta sử dụng: `dir(obj)`. Ví dụ:


```python
# Giả sử ta có list 
m1 = [1, 2, 3]

# Các hàm đặc trưng
dir(m1)
```




    ['__add__',
     '__class__',
     '__class_getitem__',
     '__contains__',
     '__delattr__',
     '__delitem__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__getitem__',
     '__gt__',
     '__hash__',
     '__iadd__',
     '__imul__',
     '__init__',
     '__init_subclass__',
     '__iter__',
     '__le__',
     '__len__',
     '__lt__',
     '__mul__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__reversed__',
     '__rmul__',
     '__setattr__',
     '__setitem__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     'append',
     'clear',
     'copy',
     'count',
     'extend',
     'index',
     'insert',
     'pop',
     'remove',
     'reverse',
     'sort']



### 5.2. String representation

Đầu tiên, giả sử ta có class Vector như sau:


```python
class Vector:
    def __init__(self, components: list):
        self.components = components

# Tạo instance
V1 = Vector([3, 6])
print(V1)
```

    <__main__.Vector object at 0x0000020B0E007AF0>
    

Thực sự thì kết quả trả về từ hàm `print()` không giúp ích gì với người sử dụng, họ đâu quan tâm vị trí bộ nhớ là gì đâu. Vì vậy, ta phải thay đổi hành vi của nó. Có hai cách để thực hiện điều này:

- Cách 1: Sử dụng `__str__`, hiển thị kết quả khi sử dụng hàm `print()`
- Cách 2: Sử dụng `__repr__`, hiển thị kết quả trong môi trường tương tác.




```python
class Vector:
    def __init__(self, components: list):
        self.components = components

    def __str__(self):
        if len(self.components) == 2:
            custom_string = "[ {}\n  {} ]".format(
                self.components[0], self.components[1]
            )
        elif len(self.components) == 3:
            custom_string = "[ {}\n  {}\n  {} ]".format(
                self.components[0], self.components[1], self.components[2]
            )
        elif len(self.components) == 4:
            custom_string = "[ {}\n  {}\n  {}\n  {} ]".format(
                self.components[0],
                self.components[1],
                self.components[2],
                self.components[3],
            )
        else:
            custom_string = "[  {}\n   {}\n  ...\n   {} ]".format(
                self.components[0], self.components[1], self.components[-1]
            )
        return custom_string

    def __repr__(self):
        return f"Vector({str(self.components)})"

# Xem kết quả nào với __str__
V1 = Vector([3, 5, 5, 2, 5])
print(V1)
```

    [  3
       5
      ...
       5 ]
    


```python
# Xem kết quả với __repr__
V2 = Vector([3, 6, 0])
V2
```




    Vector([3, 6, 0])



## 6. Property decorators

### 6.1. Property

Property decorators là một phương thức, giúp chúng ta truy cập vào các methods trong class như một thuộc tính. Ví dụ:


```python
# Class
class Employee:

    def __init__(self, first, last):
        self.first = first
        self.last = last

    @property
    def email(self):
        return '{}.{}@email.com'.format(self.first, self.last)

    @property
    def fullname(self):
        return '{} {}'.format(self.first, self.last)

# Truy cập vào email và fullname như một thuộc tính
emp_1 = Employee('John', 'Smith')
print(emp_1.first)
print(emp_1.email)
print(emp_1.fullname)
```

    John
    John.Smith@email.com
    John Smith
    

### 6.2. Setter

Với những phương thức được sử dụng như một thuộc tính, ta không thể thay đổi giá trị của nó như một thuộc tính, nếu không sẽ gặp phải lỗi:


```python
emp_1.fullname = "Andy Kieu"
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_1960/2394987829.py in <module>
    ----> 1 emp_1.fullname = "Andy Kieu"
    

    AttributeError: can't set attribute 'fullname'


Nếu bạn vẫn muốn thay đổi, ta phải khai báo nó dưới phương thức setter:


```python
# Class
class Employee:

    def __init__(self, first, last):
        self.first = first
        self.last = last

    @property
    def email(self):
        return '{}.{}@email.com'.format(self.first, self.last)

    @property
    def fullname(self):
        return '{} {}'.format(self.first, self.last)
    
    @fullname.setter
    def fullname(self, name):
        first, last = name.split(' ')
        self.first = first
        self.last = last
```


```python
# Kết quả
emp_1 = Employee('John', 'Smith')
emp_1.fullname = "Corey Schafer"

print(emp_1.first)
print(emp_1.email)
print(emp_1.fullname)
```

    Corey
    Corey.Schafer@email.com
    Corey Schafer
    

## 7. Tóm tắt

- Một class sẽ có các phương thức và thuộc tính.
- Định nghĩa các thuộc tính với `__init__(self, args)`
- Tạo một instance với `class_name(args)`
- Mỗi class có hai loại biến: class variable và instance variable.
- Mỗi class có 3 loại phương thức: instance method _(self)_, class method _(cls)_ và static method.
- Class method không được tác động vào đối tượng `self`, thường được sử dụng trong việc tạo instance.
- Kế thừa các thuộc tính của class cơ sở: `super().__init__(args)` hoặc `Class_name.__init__(self, args)`
- Kế thừa các phương thức của class cơ sở: `super().method(args)` hoặc `Class_name.method(self, args)`
- Nạp chồng toán tử là ghi đè hành vi của các toán tử. Sử dụng `__str__` để ghi đè hành vi của hàm `print()` và `__repr__` để ghi đè hành vi hiển thị kết quả trong môi trường tương tác.
- Property decorators giúp chúng ta truy cập vào các phương thức giống như một thuộc tính, đổi lại ta không thể gán giá trị cho những phương thức này. Để gán giá trị ta phải sử dụng setter.
