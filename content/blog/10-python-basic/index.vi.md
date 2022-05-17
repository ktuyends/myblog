---
title: "Làm quen với lập trình Python"
subtitle: ""
slug: python-basic
summary: ""
date: 2022-05-15
lastmod: 2022-05-15
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
Bài viết này, nói sao ta, ừm...có thể gọi là một cái ghi chép mình tóm tắt lại một số kiến thức cơ bản trong Python. Vì đôi lúc, mình cũng sẽ cần đọc lại chúng. Với cả, mục đích chính mình viết cái ghi chép này là viết cho bạn của mình, chứ thực ra mình cũng đã viết một [Series - Python Programming](/python-programming/) rồi nhưng vì là viết cho chính mình nên nó khá là khó hiểu.

Trước khi đi vào nội dung chính, thì ta cần phải cài đặt Python. Có một số cách sau:

- Cách 1: Sử dụng [Python Online Compiler](https://replit.com/) mà không cần cài đặt.
- Cách 2: Tải và cài đặt Python từ [Download](https://www.python.org/downloads/).
- Cách 3: Cài đặt [Anaconda](https://www.anaconda.com/products/distribution) sau đó sử dụng Ipython hoặc Jupyter Lab.

Còn về bài viết này, thì mình sử dụng Jupyter Notebook trên VS Code.

## 1. Biến và phép gán

### 1.1. Biến

Trong Python, mọi thứ đều là đối tượng, và biến trong Python ta hiểu nôm na nó là một cái tên, trỏ đến một đối tượng nào đó. Khi một đối tượng được gán cho một biến, ta có thể sử dụng tên biến để đại diện cho đối tượng ở nhiều nơi ví dụ trong các phép toán.

Để gán một đối tượng cho một biến ta sử dụng cú pháp: `ten_bien = gia_tri`. Ví dụ:


```python
# Phép gán
my_var = 100

# xem địa chỉ trong bộ nhớ của my_var
print(id(my_var))
```

    2085885447504
    


```python
# Xem kiểu dữ liệu của biến
type(my_var)
```




    int



{{< admonition type=notes title="Một số lưu ý về tên biến" open=true >}}
- Tên biến trong Python chỉ bao gồm các chữ cái `a-zA-Z`, chữ số `0-9` và dấu gạch dưới `_`.
- Tên biến phân biệt giữa các ký tự in hoa và in thường.
- Tên biến không được trùng với các từ khóa trong Python.
- Tên biến không được bắt đầu bằng số.
- Tên biến nên là các từ có ý nghĩa thay vì các chữ cái.
{{< /admonition >}}

### 1.2. Phép gán

Một số cách sử dụng phép gán trong Python:

```python
# Gán một giá trị cho một biến
my_var = 10

# Gán một giá trị cho nhiều biến
a = b = c = 10

# Gán nhiều giá trị cho nhiều biến
a, b = (5, 10)
a, b = 5, 10      # a = 5, b = 10

# Lưu ý với string
a, b, c, d, e, f = 'Python'
print(a) # 'P'

# đổi giá trị giữa 2 biến
x = 5
y = 10
x, y = y, x  # x = 10, y = 5
```

### 1.3. Input và Print

- Hàm `input()`: Yêu cầu người dùng nhập giá trị cho một biến. Kết quả của hàm `input` là kiểu string.
- Hàm `print()`: Được sử dụng để in giá trị của một đối tượng, biến, biểu thức,...ra màn hình.

Ví dụ:


```python
print('Hello, world!')
print('What is your name?')
```

    Hello, world!
    What is your name?
    


```python
# Nhập tên cho biến my_name
my_name = input('What is your name?')
print('It is good to meet you,', my_name)
```

    It is good to meet you, Andy
    

### 1.4. Comment 

Nếu để ý, các bạn có thể thấy trong code của mình hay có đoạn như `# một cái gì đó`, thì trong Python nó được gọi là **Comment**. 

Comment là những ghi chú mà chương trình sẽ bỏ qua khi thực thi. Thông thường, một ghi chú sẽ bắt đầu từ dấu `#` cho đến cuối dòng code.

## 2. Kiểu dữ liệu strings

### 2.1. Tạo strings

Strings trong Python là một chuỗi các ký tự. Ta có thể liên tưởng đến các chữ cái, các từ, các câu trong đời sống thường ngày mà chúng ta hay dùng vậy.

Để tạo một strings, ta đặc các ký tự bên trong dấu `'...'` hoặc dấu `"..."`. Ví dụ:


```python
# Sử dụng dấu '...'
message = 'Hello World'
print(message)
```

    Hello World
    


```python
# Lưu ý khi sử dụng dấu `'...'` mà bên trong chuỗi cũng có dấu `'`
message = 'Andy's World'

# Trong trường hợp này sẽ gặp lỗi
print(message)
```


      File "C:\Users\ktuyends\AppData\Local\Temp/ipykernel_16852/1432468934.py", line 2
        message = 'Andy's World'
                               ^
    SyntaxError: unterminated string literal (detected at line 2)
    



```python
# Để sửa lỗi ta có hai cách:
# Cách 1: Đặt string bên trong "..."
message = "Andy's World"
print(message)
```

    Andy's World
    


```python
# Cách 2: Sử dụng ký tự thoát `\` bên trong string để giải thích cho chương trình `'` là một dấu `'`
message = "Andy\'s World"
print(message)
```

    Andy's World
    

Việc sử dụng dấu ngoặc `'...'` hoặc `"..."` chỉ cho phép chúng ta tạo ra các strings trên một dòng. Trong trường hợp ta muốn tạo các strings có nhiều dòng thì làm như thế nào? Ví dụ:


```python
# Chúng ta sử dụng """...""" để viết các string trên nhiều dòng
message = """Bobby's World was a good
cartoon in the 1990s
"""

# Xem kết quả nào
print(message)
```

    Bobby's World was a good
    cartoon in the 1990s
    
    

### 2.2. Truy cập các ký tự trong string

Mỗi một chuỗi ký tự đều có số lượng ký tự nhất định, và để xem một chuỗi các ký tự có nhiêu ký tự thì ta sử dụng hàm `len()`, ví dụ:


```python
# Giả sử ta có chuỗi sau
message = 'Monty Python'

# Tính số lượng các ký tự trong message
message_len = len(message)
print(message_len)
```

    12
    

Mỗi một ký tự trong Python đếu có một index, được đánh số bắt đầu từ `0 -> len(my_str) - 1` nếu tính từ bên trái hoặc bắt đầu từ `-1 -> - len(my_str)` nếu tính từ bên phải. Minh họa:

{{< figure src="./string-index.jfif" >}}

Bây giờ sau khi đã xác định được vị trí của mỗi ký tự, ta có thể lấy ra các ký tự này bên trong string dựa vào vị trí của nó với cú pháp:

```python
# Lấy ra ký tự ở vị trí i
my_string[i]

# Lấy ra một chuỗi con từ trong string
# Lấy ra các ký tự từ start -> end - 1, Python không lấy ký tự cuối.
my_string[start:end]

# Tổng quát: start:end :step
# step là bước nhảy, ví dụ start = 1, step = 2
# Thì ta có các ký tự ở vị trí 1, 3, 5, 7,....
```


```python
# Giả sử ta có chuỗi sau
message = 'Monty Python'

# Ký tự thứ 7 trong chuỗi
message[6]
```




    'P'




```python
# Các ký tự từ vị trí thứ 6 -> 9
message[6:10]
```




    'Pyth'




```python
# Các ký tự từ -12 -> -8
message[-12:-7]
```




    'Monty'




```python
# Các ký tự ở vị trí 0, 2, 4, 6,...
message[0:12:2]
```




    'MnyPto'



Lưu ý, trong trường hợp `start` hoặc `end` bỏ trống, thì Python mặc định là tính từ đầu chuỗi hoặc đến cuối chuỗi, `step` mặc định là `1`. Ví dụ:


```python
# Các ký tự từ vị trí thứ 6 đến cuối chuỗi
message[6:]
```




    'Python'



### 2.3. Một số phương thức làm việc với string

Nhắc lại trong Python, mọi thứ đều là đối tượng và string cũng thế. Tạm thời ta chưa cần quan tâm đối tượng là gì, nhưng ta có thể hiểu nôm na là một đối tượng sẽ có các phương thức (method) và thuộc tính (attribute). Phương thức là các hàm tác động lên đối tượng, còn thuộc tính thì là đặc tính của đối tượng.

Để sử dụng phương thức ta dùng cú pháp: `my_string.method_name()`

Một số phương thức cơ bản:

```python
# Giả sử ta có chuỗi
message = 'Hello World

# Chuyển đổi giữa các ký tự in hoa và in thường
message.lower()     # hello world
message.upper()     # HELLO WORLD
message.title()     # Hello world

# Đếm số lần xuất hiện của một substring trong chuỗi
message.count('Hello')  # 1 lần
message.count('l')      # 3 lần

# Xác định vị trí bắt đầu của một substring trong chuỗi
# find trả về -1 nếu k tìm thấy
message.find('World')   # 6

# Thay thế một số ký tự trong string
# replace(old_substring, new_substr)
new_message = message.replace('World', 'Universe')   # Hello Universe

# Nối các ký tự với toán tử '+'
greeting = 'Hello'
name = 'Andy'
message = greeting + ' ' + 'Andy'   # Hello Andy

# Toán tử '+' đôi khi phức tạp khi câu lệnh dài
# Ta có thể sử dụng f-string
message = f'{greeting}, {name}. Welcome!'  # Hello, Andy. Welcome!

# Nếu ta thêm dấu = vào trong ngoặc kép, ví dụ:
message = f'{name = }'  # name = 'Andy'
```

{{< admonition type=notes title="Immutable" open=true >}}
Lưu ý, string là kiểu dữ liệu `immutable`, vì thế ta không thể thực hiện các thao tác sửa đổi lên trực tiếp string ban đầu. Do đó, các phương thức cũng không sửa đổi string gốc mà nó sẽ trả về một string khác.
{{< /admonition >}}

Ngoài các phương thức trên, còn rất nhiều các phương thức để làm việc với string mà ta có thể sử dụng `help()` để xem:

```python
# Xem trợ giúp về kiểu dữ liệu string
print(help(str))
```

## 3. Kiểu dữ liệu số

### 3.1. Int và float

Số trong Python thường được biểu diễn dưới dạng số nguyên _(int)_ hoặc số thực _(float)_. Số nguyên là số nguyên trong toán học, còn số thực là các số mà có thêm phần thập phân (dấu chấm phân tách). Ví dụ:


```python
# Số nguyên
num = 10
print(type(num))
```

    <class 'int'>
    


```python
# Số thực
Pi = 3.14
print(type(Pi))
```

    <class 'float'>
    

### 3.2. Các toán tử cơ bản

Một số phép toán giữa các số:

```python
3 + 2   # Phép cộng
3 - 2   # Phép trừ
3 * 2   # Phép nhân
3 / 2   # Phép chia
3 // 2  # Phép chia lấy phần nguyên
3 % 2   # Phép chia lấy phần dư (mod)
3 ** 2  # Lũy thừa
```

Một số phép so sánh. Lưu ý kết quả của các phép so sánh sẽ trả về `True` hoặc `False`

```python
3 > 2    # True (so sánh lớn hơn)
3 >= 2   # True (lớn hơn hoặc bằng)
3 < 2    # False (nhỏ hơn)
3 <= 2   # False (nhỏ hơn hoặc bằng)
3 == 2   # False (so sánh bằng)
3 != 2   # True (so sánh không bằng)
```

### 3.3. Các hàm làm việc với số

```python
abs(-3)            # Giá trị tuyệt đối
round(3.75, 1)     # 3.8, Làm tròn số, gần số chẵn nhất
round(3.65, 1)     # 3.6
```

Có nhiều hàm không có sẵn trong Python, vì vậy ta cần phải sử dụng các thư viện mở rộng bên ngoài. **Math** là module gồm nhiều hàm toán học để làm việc với các số. 

```python
# import thư viện trước khi sử dụng
import math

# Sử dụng các hàm bởi cú pháp: math.func_name()
math.trunc(x)   # phần nguyên của một số
math.floor(x)   # số được làm tròn > x
math.ceil(x)    # số được làm tròn < x
math.fabs(x)    # giá trị tuyệt đối
math.sqrt(x)    # căn bậc hai
```

**Lưu ý khi so sánh 2 số thực:**

Số thực trong Python là số ở dạng xấp xỉ, vì vậy khi ta so sánh một biểu thức trả về kết quả là một số thực với một số thực có thể sẽ không bằng nhau. Ví dụ:


```python
# Lưu ý khi so sánh hai số thực
0.1 + 0.2 == 0.3 # False
```




    False




```python
# Để so sánh hai số thực ta sử dụng hàm math.isclose
import math
math.isclose(0.1 + 0.2, 0.3)
```




    True



### 3.4. Chuyển đổi kiểu dữ liệu

Đôi lúc chúng ta sẽ cần chuyển đổi qua lại giữa các kiểu dữ liệu. Ví dụ bạn yêu cầu một người nhập một giá trị số bằng hàm `input()` nhưng mà hàm `input()` lại trả về kiểu `str` (string), khi đó ta phải chuyển đổi nó về kiểu `float` hoặc `int` để tính toán.

```python
# Chuyển đổi string thành number
my_str = '100'
float(my_str)   # Chuyển đổi về số thực bằng hàm float()
int(my_str)     # Chuyển đổi về số nguyên bằng hàm int()

# Chuyển đổi một số thành string
my_num = 7749
str(my_num)     # Chuyển đổi về string bằng hàm str()
```

## 4. Lists, Tuples và Sets

### 4.1. Lists

List là một trong những cấu trúc dữ liệu linh hoạt nhất trong Python, nó được sử dụng để lưu trữ nhiều giá trị. Giả sử ta muốn lưu trữ một danh sách các môn học vào một list. Ta sẽ tạo ra một list bằng cách sử dụng cú pháp `[item1, item2, .., itemN]`, mỗi item tương ứng với một môn học và các môn học được ngăn cách bởi dấu `,`

```python
# Tạo một list các môn học
courses = ['History', 'Math', 'Physics', 'CompSci']

# Để xem có bao nhiêu môn học ta sử dụng hàm len
len(courses)  # 4 môn
```

Hãy nhớ lại cách chúng ta lấy ra các ký tự trong một string, thì tương tự ta cũng có thể sử dụng cú pháp đó để lấy ra các phần tử bên trong một list.

```python
# Xem môn học đầu tiên
courses[0]   # History

# Xem môn học cuối cùng
courses[-1]  # CompSci

# Hai môn học đầu tiên
courses[0:2]  # ['History', 'Math']

# Chúng ta có thể thay đổi giá trị trong list dựa vào index
courses[0] = 'Programming'
```

Bây giờ, chúng ta muốn thêm một môn học `Art` vào trong list trên, ta có một số cách sau:

```python
# Thêm một môn học Art vào cuối danh sách
courses.append('Art')
print(courses)   # ['History', 'Math', 'Physics', 'CompSci', 'Art']

# Thêm vào một vị trí xác định trong danh sách
courses.insert(1, 'Art')

# append và insert chỉ thêm được một môn học
# Nếu muốn thêm nhiều môn học vào trong danh sách sử dụng extend
# Extend sẽ thêm vào cuối danh sách
courses.extend(['Art', 'Education'])
```

{{< admonition type=notes title="Mutable và Immutable" open=true >}}
Các bạn có phát hiện ra điều gì lạ ở ví dụ trên không. Khi chúng ta sử dụng các phương thức với strings, thì nó không thay đổi string mà tạo ra một string mới. Ngược lại với list, nó lại áp dụng trực tiếp các thay đổi vào list ban đầu. Điều này là bởi vì list là cấu trúc dữ liệu dạng `mutable`. **Mutable** là cấu trúc dữ liệu mà ta có thể thực hiện các thao tác sửa đổi đối với đối tượng ban đầu.

Trong Python:

- Cấu trúc dữ liệu Mutable gồm có: List, Dictionary, Set.
- Cấu trúc dữ liệu Immutable gồm có: String, Tuple.
{{< /admonition >}}

Sau khi nhìn lại danh sách trên, bạn chợt phát hiện ra mình thêm nhầm môn học và muốn xóa chúng đi thì ta cũng có một số cách như sau:

```python
# Danh sách môn học
courses = ['History', 'Math', 'Physics', 'CompSci']

# Xóa một môn học khỏi danh sách
courses.remove('Math')

# Xóa môn học cuối cùng, và trả về môn học bị xóa
courses.pop()  # CompSci
```

Một số phương thức khác làm việc với list:

```python
# Xem một phần tử có nằm trong list hay không
'Physics' in courses  # True

# Nếu phần tử nằm trong list, ta đi
# Xác định vị trí của phần tử đó
courses.index('Physics')  # 2
```

```python
# Đảo ngược thứ tự các phần tử trong list
courses.reverse()

# Sắp xếp các phần tử
# reverse = FALSE là mặc định sắp xếp tăng dần
courses.sort(reverse = FALSE)

# Sắp xếp các phần tử mà không thay đổi list gốc
# sorted() sẽ tạo ra một list mới được sắp xếp
sorted(courses)

# Giá trị nhỏ nhất, lớn nhất, tổng
nums = [1, 7, 4, 10, 12]
min(nums)   # 1
max(nums)   # 12
sum(nums)   # 34
```

Nội dung cuối cùng về list, bây giờ ta muốn chuyển tất cả các môn học trong danh sách trên thành một câu thay vì tách rời nhau thành các phần tử. 

```python
# Phương thức join
# 'chr' là ký tự phân tách các phần tử trong câu
# 'chr'.join([my_list])
course_str = ', '.join(courses) 
print(course_str)  # 'History, Math, Physics, CompSci' 

# Chuyển đổi ngược lại string thành list
new_list = course_str.split(', ')
print(new_list)
```

### 4.2. Tuples

Tuples về cơ bản là giống với list, chúng ta có thể thực hiện các thao tác truy cập vào tuples và lấy ra các phần tử. Nhưng cũng có một số điểm khác biệt như:

- Tuples được tạo bởi các phần tử bên trong `(...)` còn list thì sử dụng `[...]`
- Tuples là Immutable, cho nên ta không thể thực hiện các thao tác và phương thức sửa đổi, làm thay đổi Tuples.


```python
# List is mutable
list_1 = ['History', 'Math', 'Physics', 'CompSci']
list_2 = list_1

# Xem kết quả của hai list
print(f'{list_1 = }')
print(f'{list_2 = }')
```

    list_1 = ['History', 'Math', 'Physics', 'CompSci']
    list_2 = ['History', 'Math', 'Physics', 'CompSci']
    


```python
# Thay đổi phần tử của list_1
list_1[0] = 'Art'

# Xem sự thay đổi trong cả hai list
print(f'{list_1 = }')
print(f'{list_2 = }')
```

    list_1 = ['Art', 'Math', 'Physics', 'CompSci']
    list_2 = ['Art', 'Math', 'Physics', 'CompSci']
    

Bây giờ ta thử tạo một tuple tương tự list và thay đổi giá trị bên trong nó:


```python
# Tuple is immutable
tuple_1 = ('History', 'Math', 'Physics', 'CompSci')
tuple_2 = tuple_1

# Xem kết quả 
print(f'{tuple_1 = }')
print(f'{tuple_2 = }')
```

    tuple_1 = ('History', 'Math', 'Physics', 'CompSci')
    tuple_2 = ('History', 'Math', 'Physics', 'CompSci')
    


```python
# Thử thay đổi giá trị bên trong tuple
tuple_1[0] = 'Art'
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_16852/2956275389.py in <module>
          1 # Thử thay đổi giá trị bên trong tuple
    ----> 2 tuple_1[0] = 'Art'
    

    TypeError: 'tuple' object does not support item assignment


### 4.3. Sets

Sets, hiểu đơn giản thì nó giống với một tập hợp gồm nhiều phần tử trong toán học. Các phần tử trong tập hợp là không có thứ tự vì thế ta không sử dụng index để truy cập và lấy ra các phần tử như với lists và tuples.

Để tạo một set, ta sử dụng cú pháp `{item1, item2,...,itemN}`



```python
# Sets
cs_courses = {'History', 'Math', 'Physics', 'CompSci', 'Math'}

# Các phần tử không theo thứ tự, không lặp lại
print(cs_courses)
```

    {'History', 'Math', 'Physics', 'CompSci'}
    


```python
# Thử truy cập các phần tử dựa vào index
print(cs_courses[0])
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_16852/3984569593.py in <module>
          1 # Thử truy cập các phần tử dựa vào index
    ----> 2 print(cs_courses[0])
    

    TypeError: 'set' object is not subscriptable



```python
# Xem một phần tử có nằm trong set hay không
'Art' in cs_courses
```




    False



Vì Sets mang ý nghĩa là các tập hợp, nên ta có thể thực hiện một số phép toán tập hợp với Sets như phép giao, phép hợp,...


```python
# Giả sử ta có hai tập hợp
cs_courses = {'History', 'Math', 'Physics', 'CompSci'}
art_courses = {'History', 'Math', 'Art', 'Design'}

# Phép giao
cs_courses.intersection(art_courses)
```




    {'History', 'Math'}




```python
# Phép hợp
cs_courses.union(art_courses)
```




    {'Art', 'CompSci', 'Design', 'History', 'Math', 'Physics'}




```python
# Phép trừ
cs_courses.difference(art_courses)
```




    {'CompSci', 'Physics'}



Một điều cuối cùng về List, Tuple và Sets.

```python
# Tạo list rỗng
empty_list = []
empty_list = list()

# Tạo tuples rỗng
empty_tuple = ()
empty_tuple = tuple()

# Tuple có một phần tử
first_tuple = 5, 
first_tuple = (5, )

# Tạo sets rỗng
# Không sử dụng {} vì đây là dictionary
empty_set = set() 
```

**Tóm lại, chúng ta:**

- Sử dụng list khi muốn thực hiện tất cả các thao tác thêm bớt, sửa đổi các phần tử.
- Sử dụng tuple nếu chỉ muốn truy cập vào các phần tử trong tuple.
- Sử dụng set để loại bỏ các giá trị trùng lặp hoặc kiểm tra xem một giá trị có nằm trong một tập hợp hay không.

## 5. Dictionaries

Khi nói về Dictionaries, ta có thể tưởng tượng nó là tập hợp các cặp giá trị bao gồm keys và values. Ví dụ cặp `'name':'Andy'` thì `name` là key còn `Andy` là value. Trong dictionary thì key là giá trị không thể thay đổi - `immutable` và không được trùng lặp với các cặp giá trị khác.

```python
# Tạo dictionary rỗng
my_dict = {}
my_dict = dict()
```


```python
# Tạo dictionary có phần tử
student = {'name': 'Andy', 'age': 28, 'course': ['Math', 'CompSci']}
print(student)
```

    {'name': 'Andy', 'age': 28, 'course': ['Math', 'CompSci']}
    

Chúng ta sử dụng các keys để truy cập vào các phần tử của dictionary.


```python
# Danh sách các key
st_key = student.keys()
print(st_key)
```

    dict_keys(['name', 'age', 'course'])
    


```python
# Truy cập vào các phần tử
# Không tìm thấy key sẽ trả về lỗi
print('Names:', student['name'])
print('Age: ', student['age'])
print('Courses: ', student['course'])
```

    Names: Andy
    Age:  28
    Courses:  ['Math', 'CompSci']
    


```python
# Tương tự ta có thể sử dụng phương thức get
# Để truy cập vào các phần tử
# Nếu không tìm thấy key, get trả về None
student.get('name')
```




    'Andy'



Tiếp theo, ta muốn thêm một phần tử mới vào trong dictionary, ta sử dụng cú pháp sau: `my_dict['new_key'] = value`


```python
# Thêm số điện thoại 
student['phone'] = '+84345025687'

# Sửa đổi tên
student['name'] = 'Sophia'
print(student)
```

    {'name': 'Sophia', 'age': 28, 'course': ['Math', 'CompSci'], 'phone': '+84345025687'}
    


```python
# Chúng ta có thể sử dụng phương thức update để thay đổi giá trị của nhiều key
# Nếu key không tồn tại sẽ được thêm vào
student.update({'name': 'Andy', 'age': '29', 'phone': '555-5555'})
print(student)
```

    {'name': 'Andy', 'course': ['Math', 'CompSci'], 'phone': '555-5555', 'age': '29'}
    

Tiếp theo, ta có thể xóa một phần tử khỏi dictionary bằng cú pháp: `del my_dict['key]` hoặc `my_dict.pop('key')` nếu muốn trả về giá trị bị xóa.


```python
# Xóa age khỏi student
del student['age']
print(student)
```

    {'name': 'Andy', 'course': ['Math', 'CompSci'], 'phone': '555-5555'}
    

**Một số phương thức và thuộc tính khác:**

```python
# Danh sách key
student.keys()

# Danh sách giá trị
student.values()

# Danh sách cặp key - value
student.items()
```

## 6. Conditionals và Booleans

### 6.1. Các toán tử so sánh

- Toán tử so sánh: _==, !=, >, >=, <, <=_
- So sánh về mặt đối tượng: _is, is not_
- Toán tử boolean: _and, or, not, and not, or not_
- Toán tử: _in, not in_

### 6.2. Cú pháp

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
    # Thực thi câu lệnh

# if rút gọn
<value_if_True> if <dieu_kien> else <value_if_False>
```

{{< admonition type=notes title="Cấu trúc Match - Case" open=false >}}
Đây là một cấu trúc mới xuất hiện trong Python 3.10. Thay vì kiểm tra các điều kiện như câu lệnh `if`, nó kiểm tra các trường hợp có thể xảy ra. Cú pháp:

```python
my_var = 10
match my_var:
    case value_1:
        # Do something
    case value_2:
        # Do something
    case _:
        # Thực hiện nếu tất cả các lệnh trên bị bỏ qua
```
{{< /admonition >}}

### 6.3. Một số lưu ý

{{< admonition type=notes title="Lưu ý 1:" open=true >}}
Khi so sánh hai iterable cùng loại, Python sẽ lấy lần lượt từng phần tử trong iterable ra để so sánh:

```python
'Kteam' == "Kteam" # True
'Free' == 'Education' # False
```
{{< /admonition >}}

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

{{< admonition type=notes title="Đối tượng singleton" open=true >}}
Theo mặc định các số nguyên từ -5 đến 256 (đối tượng singleton) được Python tạo sẵn, vì vậy nó có địa chỉ xác định. Nên khi ta sử dụng toán tử `is` để so sánh hoặc sử dụng `id(num)` để kiểm tra vị trí thì nó luôn cố định.

Một số đối tượng singleton khác như: *True, False, None*. Với những đối tượng này, ta nên sử dụng toán tử `is` thay vì sử dụng `==`.
{{< /admonition >}}

{{< admonition type=notes title="Kiểu boolean" open=true >}}
Khi nhắc đến kiểu dữ liệu boolean, mọi thứ biểu thị giá trị `0`, rỗng, `None`,...sẽ được hiểu là False. Ngược lại là True.

```python
bool(0), bool(-1), bool(1), bool(100) # (False, True, True, True)
bool(None) # False
```
{{< /admonition >}}


## 7. Loops và Iterations

### 7.1. Vòng lặp for

```python
# Cú pháp
# iterable: string, list, tuple, dictionary, set, range()
# iterable: Là một đối tượng, có khả năng lặp qua từng phần tử 
for var in iterable:
    # Thực thi các câu lệnh

else: # Có thể có hoặc không
    # Nếu vòng lặp không bị break
    # Thì thực thi else sau khi kết thúc vòng lặp 
```

### 7.2. Vòng lặp while

```python
# Cú pháp
while <dieu_kien>:
    # Thực thi cho đến khi điều kiện trả về False

else: # Có thể có hoặc không
    # Nếu vòng lặp không bị break
    # Thì thực thi else sau khi kết thúc vòng lặp 
```
### 7.3. break, continue và pass

- break: thoát khỏi vòng lặp trong cùng chứa nó.
- continue: thoát khỏi lượt lặp hiện tại, chuyển sang lượt lặp tiếp theo.
- pass: Không thực thi gì hết, chỉ mang ý nghĩa giữ chỗ.

> Nếu sử dụng câu lệnh `try-finally` bên trong vòng lặp, thì `finally` luôn luôn thực thi, dù cho vòng lặp gặp phải break hoặc continue.

### 7.4. range, zip và enumerate



```python
# range(n) tạo ra một dãy số từ 0 -> n-1
for i in range(4):
    print(i)
```

    0
    1
    2
    3
    


```python
# range(start, end) tạo ra một dãy số từ start đến end-1
for i in range(2, 6):
    print(i)
```

    2
    3
    4
    5
    


```python
# zip() kết hợp các phần tử ở vị trí tương ứng của iterator
a = ['a', 'b', 'c']
b = [5, 10, 15]

# for với zip()
# zip(a, b) = [('a', 5), ('b', 10), ('c', 15)]
for (m, n) in zip(a, b):
    print(m, n)
```

    a 5
    b 10
    c 15
    


```python
# enumerate tạo ra một list các cặp (index, value)
my_list = ['monday', 'tuesday', 'sunday']
# enumerate(my_list) = [(0, 'monday'), (1, 'tuesday'), (2, 'sunday')]

for key, value in enumerate(my_list):
    print(key, value)
```

    0 monday
    1 tuesday
    2 sunday
    

## 8. Functions

Functions ta có thể hiểu đơn giản giống như các hàm trong toán học, nó nhận vào một số tham số sau đó thực hiện tính toán và trả về một giá trị nào đó. 

Chúng ta thường sử dụng hàm khi muốn gom nhiều dòng code có khả năng sử dụng lặp đi lặp lại nhiều lần. Khi đó ta chỉ cần gọi hàm thay vì phải code lại từ đầu tất cả mọi thứ.  

### 8.1. Tạo hàm

Cú pháp:

```python
# function_name là tên hàm
# parameters là các tham số của hàm
# my_results là kết quả mà hàm trả về
def function_name(parameters):
    # Do something
    return my_result
```

Chúng ta hãy bắt đầu với một hàm đơn giản không chứa tham số nào hết:

```python
# Định nghĩa hàm hello_func()
def hello_func():
    # pass: không làm gì hết, chỉ mang ý nghĩa giữ chỗ
    pass

# Gọi hàm:
hello_func()
```

Bây giờ chúng ta sẽ thêm một cái gì đó vào hàm, ví dụ một câu chào:


```python
# Thêm nội dung vào function
def hello_func():
    print('Hello Function!')

# Thử chạy nào
hello_func()
```

    Hello Function!
    


```python
# Thay vì sử dụng hàm print ta sử dụng return
def hello_func():
    return 'Hello Function!'

# Thử chạy nào
hello_func()
```




    'Hello Function!'



Bây giờ, thay vì trả về một câu chào như `Hello Function!`, bạn muốn hàm của chúng ta có thể trả về những câu khác mà bạn truyền vào hàm. Ta cần sửa đổi một chút:


```python
# Thêm các tham số
def hello_func(greeting):
    return f'{greeting} Function!'

# Chạy thử nào
hello_func('Hi')
```




    'Hi Function!'




```python
# Thêm tham số mới
def hello_func(greeting, name):
    return f'{greeting}, {name}'

# Gọi hàm
hello_func('Hello', 'Andy')
```




    'Hello, Andy'



Hàm có thể có các tham số mang giá trị mặc định, mà khi gọi hàm nếu ta không truyền giá trị cho nó thì nó sẽ sử dụng giá trị này, ngược lại nếu ta truyền giá trị cho nó thì nó sẽ sử dụng giá trị được truyền vào.


```python
# Hàm với tham số có giá trị mặc định
def hello_func(greeting, name = "Peace"):
    return f'{greeting}, {name}'

# Gọi hàm mà không truyền tham số cho name
hello_func('Hi')
```




    'Hi, Peace'



### 8.2. *args và **kwargs

Đôi khi bạn sẽ gặp các hàm với tham số là `*args` và `**kwargs` thì ta có thể hiểu đơn giản thế này: Hai tham số này, đại diện cho số lượng các tham số không được xác định khi truyền vào hàm, nghĩa là ta có thể truyền bao nhiêu tùy ý. 

_**Args**_ thường đại diện cho một tuple, và **_kwargs_** thường đại diện cho một dictionary. Trước khi đi vào giải thích hai đối số này ta làm quen với khái niệm _unpacking_:


```python
# Giả sử ta có một tuple như sau:
fruits = ("apple", "banana", "cherry")

# Unpacking tuple
green, yellow, red = fruits

# Kết quả
print(f'{green = }')
print(f'{yellow = }')
print(f'{red = }')
```

    green = 'apple'
    yellow = 'banana'
    red = 'cherry'
    


```python
# Unpacking sử dụng *
# Giả sử ta có tuple
fruits = ("apple", "banana", "cherry", "strawberry", "raspberry")
(green, yellow, *red) = fruits

# Xem kết quả
# Kết quả
print(f'{green = }')
print(f'{yellow = }')


# 
print(f'{red = }')
print('*read = ', *red)
```

    green = 'apple'
    yellow = 'banana'
    red = ['cherry', 'strawberry', 'raspberry']
    *read =  cherry strawberry raspberry
    

Như bạn thấy, giả sử args là một tuple, thì khi ta unpacking nó vào trong hàm với `*args`, thì mỗi một phần tử của tuple sẽ trở thành một tham số của hàm. Tương tự thì `**kwargs` cũng hoạt động giống như vậy, nhưng vì kwargs là dictionary, nên nó sẽ trở thành các tham số mang giá trị mặc định (keys trở thành tham số, values trở thành giá trị mặc định của tham số đó).


```python
# Ví dụ
def student_info(*args, **kwargs):
    print(args)
    print(kwargs)

# Khi ta truyền tham số
# Những tham số không sử dụng key sẽ là một phần tử của args
# Những tham số mà sử dụng key sẽ thành một phần tử của kwargs
student_info('Math', 'Art', name = 'Andy', age = 22)
```

    ('Math', 'Art')
    {'name': 'Andy', 'age': 22}
    


```python
# Ta cũng có thể truyền các tham số kiểu args và kwargs
course = ['Math', 'Art']
info = {'name': 'Andy', 'age': 25}
student_info(*course, **info)
```

    ('Math', 'Art')
    {'name': 'Andy', 'age': 25}
    

### 8.3. Hàm ẩn danh lambda

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

### 8.4. Map và filter

Một hàm nhận một hàm khác làm đối số, hoặc trả về một hàm được gọi là _higher-order functions_.

**Hàm Map**

Cú pháp:

```python
# Áp dụng một hàm cho từng phần tử của iterable
map(func, iterable)

# Ví dụ 1
def fact(n):
    return 1 if n < 2 else n * fact(n-1)

# Hàm map trả về một đối tượng map
# Vì vậy phải dùng list để xem kết quả
l = list(map(fact, [1, 2, 3, 4, 5]))
```

```python
# Ví dụ 2, kết hợp map với lambda
l1 = [1, 2, 3, 4, 5]
l2 = [10, 20, 30, 40, 50]
m = map(lambda x, y: x+y, l1, l2)
list(m)
```

**Hàm Filter**

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

## 9. List comprehension

List comprehension hiểu đơn giản là cách ta viết lại các dòng code ở dạng ngắn gọn hơn.

### 9.1. Cú pháp đơn giản

```python
# Dạng 1: Đơn giản
[Expression for var in iterable]
```

Ví dụ:

```python
# Giả sử ta có list
nums = [1, 2, 3, 4, 5, 6, 7, 8]

# Viết bình thường
my_list = []
for n in nums:
    nums.append(n*n)

# Viết bằng list comprehension
my_list = [n*n for n in nums]

# Viết bằng map + lambda
my_list = map(lambda n: n*n, nums)
```

### 9.2. List comprehension với if

```python
# Dạng 2: Một điều kiện if
[Expression for var in iterable if conditional]

# Nhiều điều kiện if
# Trả về giá trị nếu tất cả các điều kiện đều đúng
output = [expression for element in list_1 if condition_1 if condition_2]
```

Ví dụ:

```python
# Giả sử ta có list
nums = [1, 2, 3, 4, 5, 6, 7, 8]

# Viết bình thường
my_list = []
for n in nums:
    if n % 2 == 0:
        my_list.append(n)

# Viết bằng list comprehension
my_list = [n for n in nums if n % 2 == 0]

# Viết bằng filter + lambda
my_list = filter(lambda n: n % 2 == 0, nums)
```

```python
list_1 = [7, 2, -8, 6, 2, 15, 4, -2, 3, 9]
list_2 = [ x for x in list_1 if x > 0 if x % 3 == 0 ]
print(list_2)
```

### 9.3. Nested list comprehension

```python
# Dạng 3: Nested list comprehension
[Expression for var in iterable for var2 in iterable2]
```

Ví dụ:

```python
# I want a (letter, num) pair for each letter in 'abcd' and each number in '0123'
my_list = []
for letter in 'abcd':
    for num in range(4):
        my_list.append((letter, num))

# Sử dụng list comprehension
my_list = [(letter, num) for letter in 'abcd' for num in range(4)]
```

### 9.4. List comprehension với if-else

```python
# Dạng 4: List comprehension with if-else
[value1 if conditional else value2 for var in iterable]
```

Ví dụ:

```python
# Viết bình thường
fruits = []
for i in range(10):
    if i % 3 == 0:
        fruits.append('mango')
    else:
        fruits.append('orange')

# List comprehension
fruits = ["mango" if i % 3 == 0 else "orange" for i in range(10)]
print(fruits)
```

### 9.5. Dict comprehension

```python
# Dictionary Comprehensions
names = ['Bruce', 'Clark', 'Peter', 'Logan', 'Wade']
heros = ['Batman', 'Superman', 'Spiderman', 'Wolverine', 'Deadpool']
# print zip(names, heros)

# I want a dict{'name': 'hero'} for each name,hero in zip(names, heros)
my_dict = {}
for name, hero in zip(names, heros):
    my_dict[name] = hero

# Dict comprehension
my_dict = {name: hero for name, hero in zip(names, heros)}
```

## 10. OOP

### 10.1. Class và Object là gì?

Trong phần này, chúng ta không đi sâu về lập trình hướng đối tượng, nói thật sự thì mình cũng không giỏi giải thích các khái niệm cho lắm. Để bắt đầu, chúng ta hãy nghĩ về những con người mà mình sẽ gọi đây là một đối tượng **_(object)_**. 

Mỗi người thì thường có những đặc tính khác nhau ví dụ như tên, tuổi, chiều cao, màu tóc,...Và đã là con người thì đa số đều sẽ có thể thực hiện được một số việc như đi bộ, chạy, nói chuyện,...

Những đặc tính của con người mình gọi là thuộc tính của đối tượng **_(attribute)_** còn những hoạt động của con người mình gọi là phương thức **_(method)_**.

Như vậy, ta có thể liên hệ đối tượng trong lập trình hướng đối tượng với các đối tượng trong thực tế ví dụ như con người, con mèo, laptop,...Và điểm chung của các đối tượng là đều gồm hai thành phần chính:

- Thuộc tính _(attribute)_: Những thông tin, đặc điểm miêu tả về đối tượng.
- Phương thức _(method)_: Những hành động mà đối tượng có thể thực hiện.

Khi các đối tượng có những đặc tính và phương thức giống nhau, ta sẽ gom chúng lại thành một lớp các đối tượng gọi là **_Class_**. Ví dụ như class con chó, class con mèo. Và đối tượng của class con chó có thể là _chó Pug, chó Poodle, chó Husky,_...

### 10.2. Tạo một class đơn giản

Quay lại với class con người, chúng ta sẽ bắt tay vào tạo một class đơn giản:


```python
class Person:
    # Tạm thời chưa thêm thông tin gì
    pass
```

Tiếp theo, chúng ta sẽ thêm các thuộc tính cho class Person ở trên bằng phương thức `__init__()`. Lưu ý định nghĩa một phương thức trong class tương tự như khi chúng ta định nghĩa một function.


```python
class Person:

    # Thêm các thuộc tính cho con người
    # Tham số đầu tiên bắt buộc phải là self
    # self đại diện cho đối tượng
    # name, age, company là thuộc tính, chúng không cần phải giống với tên tham số
    def __init__(self, name, age, company):
        self.name = name
        self.age = age
        self.company = company
```

Bây giờ, class `Person ` đã hoàn thành, ta có thể tạo ra các đối tượng của class như sau _(instance)_:


```python
# First person
Andy = Person('Andy', 28, 'First Bank')
```


```python
# Xem các thuộc tính của đối tượng object.attribute
print(Andy.name)
print(Andy.age)
print(Andy.company)
```

    Andy
    28
    First Bank
    

### 10.3. Biến class và biến instance


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

{{< admonition type=notes title="Lưu ý" open=true >}}
Nếu chúng ta sửa giá trị của biến class ở cấp độ instance, nghĩa là sử dụng từ khóa `obj.class_attribute` thì nó chỉ thay đổi giá trị của `obj` bị sửa chứ không thay đổi giá trị của các đối tượng khác. Nếu muốn sửa giá trị của biến class cho tất cả các đối tượng ta phải sử dụng `class_name.class_attribute`.
{{< /admonition >}}

### 10.4. Phương thức

Cho đến nay, chúng ta mới chỉ tạo ra các class có thuộc tính, nhưng lại chưa có phương thức. Trong phần này, ta sẽ đi tìm hiểu cách tạo một phương thức cho class.

Các bước tạo method tương tự như khi chúng ta tạo functions chỉ khác nhau là tham số đầu tiên của method luôn luôn là `self`, hiểu nôm na thì `self` là một đối tượng của class.

Ví dụ:

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
        return math.sqrt(self.x ** 2 + self.y ** 2)

# Kết quả
import math
point_1 = Point()
point_1.set_coords(3, 4)
point_1.x # 3
point_1.y # 4
point_1.distance_to_origin() # 5
```

### 10.5. Kế thừa

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

**Thêm thuộc tính**

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

**Thêm methods**

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

**Sửa methods của class cha**

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

**Một số lưu ý**

Chúng ta sử dụng `super()` để đại diện cho class cha, khi đó ta không cần kèm theo từ khóa `self` ở đầu phương thức nữa.

Khi muốn ghi đè một hoặc một phần của một phương thức nào đó trong class cha, ta chỉ cần định nghĩa một phương thức mới trong class hiện tại với tên giống phương thức trong class cha.

## 11. Try - Except

### 11.1. Exception là gì?

Exception hiểu đơn giản thì nó là các ngoại lệ, khi chương trình gặp phải một lỗi nào đó, nó sẽ dừng lại và đưa ra các ngoại lệ kèm theo thông báo về lỗi mà chúng ta gặp phải. Ví dụ:



```python
# Lỗi chia cho số 0: ZeroDivisionError
10 / 0
```


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_1648/2762118699.py in <module>
          1 # Lỗi chia cho số 0: ZeroDivisionError
    ----> 2 10 / 0
    

    ZeroDivisionError: division by zero


### 11.2. Ví dụ đơn giản

Đầu tiên, chúng ta sẽ làm quen với câu lệnh `try-except`. Với câu lệnh này, chúng ta đặt những đoạn code mà có khả năng gặp phải lỗi khi chạy vào mệnh dề `try`, và các phản hồi khi gặp lỗi vào mệnh đề `except`. Nếu các đoạn code trong mệnh đề `try` chạy bình thường, các câu lệnh trong mệnh đề `except` sẽ không cần chạy, ngược lại nếu chương trình gặp lỗi nó dừng lại và chuyển đến chạy các câu lệnh trong mệnh đề `except`.


```python
# Hàm tính diện tích
def calcArea(radius):
    pi = 3.1416    
    radius = float(radius)
    area = pi * radius ** 2
    return area

# Xử lý với try-except
for radius in [5, "a", 4, 8, "b", 0]: 
    try: 
        area = calcArea(radius)
        print(f"Area for radius {radius} = {area}\n")
    except Exception as e:
        print(f"Something is wrong with {radius}\n")
```

    Area for radius 5 = 78.53999999999999
    
    Something is wrong with a
    
    Area for radius 4 = 50.2656
    
    Area for radius 8 = 201.0624
    
    Something is wrong with b
    
    Area for radius 0 = 0.0
    
    

### 11.3. Mở rộng cú pháp

Trong phần này, ta sẽ mở rộng `try-except` thành `try-except-else-finally`:

- _else_: Các câu lệnh trong mệnh đề này sẽ được thực thi nếu không có exception.
- _finally_: Các câu lệnh trong mệnh đề này luôn luôn được thực thi.


```python
from datetime import datetime

for radius in [5, "a", 4, 8, "b", 0]: 
    try: 
        area = calcArea(radius)
        
    except Exception as e:
        area = None
        print(f"Something is wrong for {radius}.")
        
    else: 
        print(f"calcArea() ran successfully for {radius}")
        
    finally:
        now = datetime.now()
        print(f"Area for input {radius} = {area} \ncalcArea() run completed on {now}\n")
```

    calcArea() ran successfully for 5
    Area for input 5 = 78.53999999999999 
    calcArea() run completed on 2022-05-17 10:57:25.759167
    
    Something is wrong for a.
    Area for input a = None 
    calcArea() run completed on 2022-05-17 10:57:25.759167
    
    calcArea() ran successfully for 4
    Area for input 4 = 50.2656 
    calcArea() run completed on 2022-05-17 10:57:25.760165
    
    calcArea() ran successfully for 8
    Area for input 8 = 201.0624 
    calcArea() run completed on 2022-05-17 10:57:25.760165
    
    Something is wrong for b.
    Area for input b = None 
    calcArea() run completed on 2022-05-17 10:57:25.760165
    
    calcArea() ran successfully for 0
    Area for input 0 = 0.0 
    calcArea() run completed on 2022-05-17 10:57:25.760165
    
    

### 11.4. Một số loại exceptions

Một số loại exceptions trong Python:

```
BaseException
 +-- SystemExit
 +-- KeyboardInterrupt
 +-- GeneratorExit
 +-- Exception
      +-- StopIteration
      +-- StopAsyncIteration
      +-- ArithmeticError
      |    +-- FloatingPointError
      |    +-- OverflowError
      |    +-- ZeroDivisionError
      +-- AssertionError
      +-- AttributeError
      +-- BufferError
      +-- EOFError
      +-- ImportError
      |    +-- ModuleNotFoundError
      +-- LookupError
```

Chúng ta bắt đầu với một ví dụ về cách except một ngoại lệ cụ thể:

```python
# Xem lại câu lệnh
except Exception as e:
    # Loại exception
    type(e).__name__

    # Thông báo lỗi
    print(e)
````

Tùy chỉnh lại chương trình trên:

```python
# Hàm đánh giá input
def validate_input(value):
    try: 
        value = float(value)
        return True
    except: return False

from datetime import datetime
for radius in [5, "a", 4, 8, "b", 0]: 
    try: 
        area = calcArea(radius)

    # Nếu gặp ValueError sẽ xử lý    
    except ValueError:
        print("Input data is not numeric type.")
        while not validate_input(radius):
            radius = input("Please input a numeric value: ")
        area = calcArea(radius)

    # Exception phải luôn bắt cuối cùng vì nó bao gồm tất cả các except khác
    # Nếu các except khác không bị bắt, sẽ bắt Exception    
    except Exception as e:
        area = None
        error_type = type(e).__name__
        print(f"Area couldn't be calculated for {radius}.")
        print(f"Error type: {error_type} \nError msg: {e}.")
        
    else: 
        print(f"calcArea() ran successfully for {radius}")
        
    finally:
        now = datetime.now()
        print(f"Area for input {radius} = {area} \ncalcArea() run completed on {now}\n")
```

### 11.5. Định nghĩa exceptions

Chúng ta hoàn toàn có thể xây dựng các exceptions theo suy nghĩ của mình, bằng cách tạo ra các class kế thừa từ class Exception:

```python
class Above50Error(Exception):
    def __init__(self, value):            
        Exception.__init__(self)
        self.value = value
        
    def __str__(self):
        return f"Input {self.value} is larger than 50 inches"
```

Để đưa ra exception tự định nghĩa, ta phải sử dụng từ khóa `raise exception_name`

```python
def calcArea(radius):
    pi = 3.1416
    radius = float(radius)
    if radius > 50:
        raise Above50Error(radius)
    else: 
        area = pi * radius ** 2
    return area
```
