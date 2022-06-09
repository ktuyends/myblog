---
title: "Pysci - Numpy"
subtitle: ""
slug: python-numpy
date: 2022-06-07
lastmod: 2022-06-07
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
series: [Python Scientific Libraries]
series_weight: 1
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
Đại số tuyến tính là một trong những nền tảng thiết yếu machine learning. Các đối tượng của đại số tuyến tính là vector và ma trận. Thư viện Numpy tất cả các công cụ cần thiết để làm việc với hai đối tượng này.

Trước khi đi tìm hiểu về Numpy, chúng ta cần phải cài đặt và import nó.

```python
# Cài đặt bằng pip
pip install numpy

# Cài đặt bằng conda
conda install numpy
```


```python
# import library
import numpy as np
```

## 1. Vector và ma trận

Array trong Python là kiểu dữ liệu chứa nhiều phần tử, trong đó các phần tử có cùng kiểu dữ liệu với nhau. Hai loại mảng được sử dụng nhiều nhất là vector và ma trận, ngoài ra còn có mảng ba chiều, mảng nhiều chiều,...

### 1.1. Vector

Để tạo một vector đơn giản nhất là chuyển đổi một list các giá trị có cùng kiểu dữ liệu thành mảng, sử dụng `np.array()`

```python
v = np.array([1., 2., 3.])
```

Bây giờ `v` đã là một vector và nó hoạt động giống như một vector trong môn đại số tuyến tính. Một số ví dụ:


```python
# Hai vector với ba phần tử
v1 = np.array([1., 2., 3.])
v2 = np.array([2, 0, 1.])

# Nhân, chia một vector với một số
print(v1 * 2)
print(v1 / 2)
```

    [2. 4. 6.]
    [0.5 1.  1.5]
    


```python
# Tổ hợp tuyến tính
print(3 * v1)
print(3 * v1 + 2 * v2)
```

    [3. 6. 9.]
    [ 7.  6. 11.]
    


```python
# norm
print(np.linalg.norm(v1))

# Tích vô hướng
np.dot(v1, v2)  # Hoặc
print(v1 @ v2)
```

    3.7416573867739413
    5.0
    

**Lưu ý**: Các phép toán số học cơ bản thực hiện trên từng phần tử.


```python
print(f'{v2 = }')
print(f'{v1 = }')
print(f'{v2 + v1 = }')
print(f'{v2 - v1 = }')
print(f'{v2 * v1 = }')
print(f'{v2 / v1 = }')

```

    v2 = array([2., 0., 1.])
    v1 = array([1., 2., 3.])
    v2 + v1 = array([3., 2., 4.])
    v2 - v1 = array([ 1., -2., -2.])
    v2 * v1 = array([2., 0., 3.])
    v2 / v1 = array([2.        , 0.        , 0.33333333])
    

### 1.2. Ma trận

Tạo một ma trận cũng tương tự như vector, nhưng tham số đầu vào của chúng ta bây giờ đổi thành một list của các list.

```python
mat = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

**Lưu ý**: Vector không phải là ma trận cột hoặc hàng, một vector có _n_ phần tử và một ma trận có số chiều `n x 1` hoặc `1 x n` là không giống nhau cho dù chúng chứa các giá trị giống nhau.


```python
# Vector v1 và số chiều
v1 = np.array([1, 2, 3])
v1.shape
```




    (3,)




```python
# Chuyển vector về ma trận cột
v1.reshape((3, 1))
```




    array([[1],
           [2],
           [3]])




```python
# Chuyển vector về ma trận hàng
v1.reshape((1, 3))
```




    array([[1, 2, 3]])



### 1.3. Indexing và slicing

Nếu các bạn đã từng học về các cấu trúc dữ liệu cơ bản trong Python như list, tuple, string,...thì về cơ bản indexing và slicing cho từng chiều trong mảng cũng tương tự như vậy.

```python
# Với vector:
vector[start:stop:step]

# Với matrix
matrix[start:stop:step, start:stop:step]
```

Ví dụ:

```python
# vector
v = np.array([1., 2., 3])
v[0]       # 1., works as for lists
v[1:]      # array([2., 3.])

# access
v[0]       # 1.
v[0] = 10

# slices
v[:2]              # array([10., 2.])
v[:2] = [0, 1]     # now v == array([0., 1., 3.])
v[:2] = [1, 2, 3]  # error!

# Matrix
M = np.array([[1., 2],
              [3., 4]])
M[0, 0]    # 1.
M[1:]      # returns the matrix array([[3., 4]])
M[1]       # returns the vector array([3., 4.])
```

### 1.4. Giải hệ phương trình tuyến tính

Trong phần trên chúng ta đã nói về toán tử `dot`:

```python
# Nhân một ma trận với một vector
np.dot(M, v)    # Kết quả là một vector
M @ v

# Tích vô hướng
np.dot(v1, v2)
v1 @ v2

# Phép nhân hai ma trận
np.dot(M1, M2)
M1 @ M2
```

Nhớ lại, giả sử ta có hệ phương trình tuyến tính \$Ax = b$, thì nghiệm của phương trình là \$x = A^{-1}b$

\$$
\begin{cases}
   x_{1} + 2x_{2} = 1 \\\\
   3x_{1} + 4x_{2} = 4
\end{cases}
$$

Chúng ta thử giải hệ phương trình này:


```python
# Tạo 2 mảng
A = np.array([
    [1., 2.],
    [3., 4.]
])

b =np.array([1., 4.])

# Sử dụng hàm solve
x = np.linalg.solve(A, b)
print(x)
```

    [ 2.  -0.5]
    

So sánh hai vector với hàm `np.allclose()`:


```python
# np.allclose
np.allclose(A @ x, b)
```




    True



## 2. Mảng trong Python

### 2.1. Thuộc tính

Trong phần trước, chúng ta đã tìm hiểu một số loại mảng phổ biến. Thì về cơ bản, một mảng trong Python sẽ có một số thuộc tính sau:

- **ndim**: Số chiều của một mảng, ví dụ vector là một chiều, ma trận là hai chiều.
- **shape**: Một tuple chứa số phần tử của mỗi chiều.
- **size**: Tổng số phần tử trong một mảng.
- **dtype**: Kiểu dữ liệu của các phần tử trong mảng.

### 2.2. Slicing

Slicing, hiểu đơn giản là từ một mảng ban đầu ta lấy ra một số phần tử nào đó dựa vào vị trí của nó, hoặc cũng có thể hiểu là việc ta tạo ra các mảng con từ mảng ban đầu. Minh họa

{{< figure src="./slicing.png" width=80% >}}

**Lưu ý:**

- Giống như các cấu trúc dữ liệu khác, chỉ số index trong mảng cũng bắt đầu từ 0 nếu tính từ trái qua phải, và bắt đầu từ `-1` nếu tính từ phải qua trái.
- Nếu kết quả slicing trả về là một phần tử thì giá trị đó là một _scalar_, nếu trả về là một cột hoặc một hàng, thì nó sẽ bị chuyển đổi thành một vector.
- Nếu chúng ta thay đổi giá trị của một mảng con được slicing, thì giá trị ở vị trí tương ứng trong mảng ban đầu của bị thay đổi theo. Cũng vì tính chất này mà chúng ta có thể sử dụng slicing để thay đổi giá trị của các phần tử bằng phép gán. Để tránh trường hợp này, hãy sử dụng phương thức `copy()`.

### 2.3. Hàm tạo mảng

Một số hàm tạo mảng được Numpy hỗ trợ:

```python
# Mảng gồm các phần tử có giá trị 0
np.zeros((n, m))   # Mảng n x m

# Mảng gồm các phần tử có giá trị 1
np.ones((n, m))    # Mảng n x m

# Mảng gồm các phần tử có giá trị q
np.full((n, m), q) # Mảng n x m

# Vector đường chéo từ ma trận x
# k là vị trí của đường chéo, mặc định k = 0, đường chéo giữa
# k > 0, đường chéo trên, k < 0 là đường chéo dưới.
# Nếu x là một vector nó trả về ma trận đường chéo
np.diag(x, k)

# Ma trận đơn vị
np.identity(n)
np.eye(n)

# Mảng các số ngẫu nhiên phân phối đều trong khoảng (0-1)
np.random.rand(n, m)   # Mảng n x m

# Mảng các số ngẫu nhiên phân phối chuẩn
np.random.normal(mu, sigma, size = (n, m))

# Mảng các số nguyên ngẫu nhiên trong khoảng [low, high)
np.random.randint(low, high, size)

# Vector các số nguyên có giá trị được sắp xếp theo thứ tự tăng dần trong khoảng [start, stop)
np.arange(start, stop, step)

# Vector gồm n phần tử cách đều nhau trong khoảng [a, b]
np.linspace(a, b, n)
```

## 3. Thay đổi cấu trúc mảng

### 3.1. Reshape

Reshape, là một phương thức giúp chúng ta thay đổi cấu trúc của một mảng với điều kiện là mảng mới phải có tổng số phần tử bằng với mảng ban đầu. Lưu ý, reshape không tạo ra mảng mới, nó chỉ thay đổi cái nhìn của chúng ta về mảng dữ liệu hiện có.

{{< figure src="./reshape.png" width=50% >}}

Ví dụ:

```python
v = array([0,1,2,3,4,5])
M = v.reshape(2,3)

M.shape # returns (2,3)

M[0,0] = 10 # now v[0] is 10
```

Đôi khi, chúng ta chỉ cần chỉ định một tham số trong `(m, n)`, tham số còn lại Numpy sẽ tự động xác định bằng cách đặt nó là `-1`. Ví dụ:




```python
v = np.array([1, 2, 3, 4, 5, 6, 7, 8])
M = v.reshape(2, -1)
M
```




    array([[1, 2, 3, 4],
           [5, 6, 7, 8]])



Ma trận chuyển vị:


```python
A = np.array([[ 1., 2.],
              [ 3., 4.]]) 
B = A.T 
print(B)
```

    [[1. 3.]
     [2. 4.]]
    

### 3.2. Stacking

{{< figure src="./stack.png" width=80% >}}

Đôi khi, chúng ta sẽ cần kết hợp các ma trận, vector lại thành một mảng mới. Có ba cách để làm điều này:

- **np.vstack**: Kết hợp theo chiều dọc.
- **np.hstack**: Kết hợp theo chiều ngang.
- **np.column_stack**: Chuyển các vector thành cột và kết hợp theo chiều ngang.

Chúng ta cũng có thể sử dụng hàm sau, đây là hàm tổng quát của ba hàm trên:

```python
# vstack, hstack
np.vstack([v1, v2])
np.hstack([v1, v2])
np.column_stack([v1, v2])

# concatenate
# axis = 0, theo chiều dọc
# axis = 1, theo chiều ngang
np.concatenate([v1, v2], axis = 0)
```

## 4. Hàm tính toán với mảng

Có nhiều hàm khác nhau được xây dựng dành cho việc tính toán với mảng. Một số hàm, tác động lên từng phần tử và trả về mảng có cùng kích thước với mảng ban đầu. Các hàm này được gọi là _ufunc - universal functions_.

Ngoài ra còn một số hàm không hoạt động theo chiều của mảng. Ví dụ như hàm _sum, min, max_, các hàm này hoạt động trên toàn bộ mảng, theo hàng hoặc theo cột. Ví dụ:

```python
# Giả sử ta có mảng
A = np.array([
    [1, 2, 3, 4],
    [5, 6, 7, 80]
])

# Hàm sum
np.sum(A)              # Trên toàn bộ mảng
np.sum(A, axis = 0)    # Theo cột
np.sum(A, axis = 1)    # Theo hàng
```

## 5. Views và Copies

### 5.1. Views

Để kiểm soát cách bộ nhớ được sử dụng, Numpy sử dụng một khái niệm là Views. Views là chế độ mà các mảng nhỏ hơn chia sẻ cùng một dữ liệu với mảng lớn hơn. Một ví dụ đơn giản nhất về Views là slicing:

```python
M = np.array([[1., 2.],
             [3., 4.]])

# first row of M
v = M[0, :] 
```

Trong ví dụ trên, `v` là một _view_ của `M`, nó và `M` tham chiếu đến cùng dữ liệu. Sửa đổi dữ liệu ở một trong hai mảng sẽ làm thay đổi dữ liệu trong mảng còn lại. Chúng ta có thể kiểm tra xem một mảng chia sẻ dữ liệu từ đâu:

```python
v.base      # array([[1.,0.],[3.,4.]])
M.base      # None, vì đây là dữ liệu của chính nó
v.base is M # True
```

Lưu ý chỉ những mảng nào slicing sử dụng `:` mới trả về một View, nếu slicing sử dụng trực tiếp các index hoặc các giá trị Boolean _(thảo luận ở phần sau)_ sẽ tạo ra một bản sao. Ví dụ:


```python
a = np.arange(4) # array([0.,1.,2.,3.])
print(a)
```

    [0 1 2 3]
    


```python
b = a[[2, 3]]
print(b)
print(b.base)
```

    [10 10]
    None
    


```python
c = a[1:3]
print(c.base)
```

    [0 1 2 3]
    

Transpose và reshape cũng tạo ra một View của mảng.

### 5.2. Copies

Đôi khi chúng ta phải sao chép một mảng để xử lý riêng biệt với mảng ban đầu, khi đó ta sẽ sử dụng phương thức `copy()` hoặc sử dụng hàm `np.array()`. Ví dụ:

```python
M = np.array([[1., 2.],
              [3., 4.]])

# Copy
N = np.array(M.T)
P = M.copy()
```

## 6. So sánh các mảng

### 6.1. Mảng boolean

Mảng _boolean_ chỉ đơn giản là một mảng mà trong đó các giá trị có kiểu _bool_ (kiểu dữ liệu chỉ có hai giá trị `True` hoặc `False`). Bất kỳ so sánh nào trên mảng sẽ tạo ra một mảng boolean.

```python
M = np.array([[2, 3],
              [1, 4]])

M > 2 # array([[False, True],
             # [False, True]])

M == 0 # array([[False, False],
             # [False, False]])

N = np.array([[2, 3],
              [0, 0]])
M == N # array([[True, True],
              # [False, False]])
```

**Lưu ý**: Vì các phép so sánh dựa trên mảng sẽ tạo ra một mảng mới, cho nên ta không thể sử dụng nó trong mệnh đề `if`. Có một giải pháp đơn giản là sử dụng `any` hoặc `all`:

```python
A = np.array([[1,2],[3,4]])
B = np.array([[1,2],[3,3]])
A == B           # creates array([[True, True], [True, False]]) 
(A == B).all()   # False
(A != B).any()   # True
```

### 6.2. Toán tử bool

Chúng ta không thể sử dụng các toán tử như `and, or, not` với mảng, mà phải sử dụng toán tử thay thế:

|Toán tử logic| Toán tử thay thế|
|:-:|:-:|
| A and B| A & B|
|A or B | A | B |
| not A | ~ A |

## 7. Indexing

Trong phần trên chúng ta đã biết cách sử dụng indexing và slicing để lấy ra các phần tử từ một mảng sử dụng các chỉ số vị trí. Trong phần này, chúng ta tìm hiểu thêm hai cách nữa để làm điều này.

### 7.1. Sử dụng mảng bool

Ví dụ:

```python
B = np.array([[True, False],
              [False, True]])
M = np.array([[2, 3],
              [1, 4]])

# indexing
M[B] # array([2,4]), a vector

# Sửa đổi giá trị
M[B] = 0
M # [[0, 3], [1, 0]]

M[B] = 10, 20
M # [[10, 3], [1, 20]]

# Thay thế các giá trị > 2 = 0
M[M > 2] = 0
```

### 7.2. Sử dụng where

Cú pháp:

```python
np.where(condition, a, b)
```

Mảng sẽ trả về các giá trị phụ thuộc vào điều kiện, nếu điều kiện trả về `True` sẽ lấy giá trị từ `a`, ngược lại sẽ lấy giá trị từ `b`. Nếu không khai báo `a, b` thì nó sẽ trả về một mảng các vị trí thỏa mãn điều kiện.


## 8. Broadcasting

Broadcasting, hiểu đơn giản là khi chúng ta thực hiện các phép tính giữa một mảng với một vector hoặc một số, thì vector và số của chúng ta sẽ tự động được mở rộng để có cùng kích thước với mảng ban đầu và sử dụng giá trị phía trước để lấp đầy khoảng trống.

{{< figure src="./broadcasting.png" width=70% >}}

Lưu ý, chiều không được mở rộng của vector phải có cùng số lượng phần tử với chiều tương ứng của mảng, nếu không sẽ gặp lỗi. Ví dụ:

{{< figure src="./miss-match.png" >}}
