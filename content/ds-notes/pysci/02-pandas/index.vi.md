---
title: "Pysci - Intro to Pandas"
subtitle: ""
slug: python-pandas
date: 2022-06-10
lastmod: 2022-06-10
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
series: [Python Scientific Libraries]
series_weight: 2
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
Pandas là thư viện quan trọng nhất theo ý kiến của nhiều nhà khoa học dữ liệu khi bạn muốn làm việc với dữ liệu trong Python. Nhiệm vụ chính của Pandas là xử lý và biến đổi dữ liệu. Trước khi đi khám phá thư viện này, chúng ta cần cài đặt và import nó:

```python
# Cài đặt bằng pip
pip install pandas

# Cài đặt bằng conda
conda install pandas
```


```python
# import pandas
import numpy as np
import pandas as pd
```

## 1. Series

{{< figure src="./series.png" width=80% >}}

Series là cấu trúc dữ liệu giống với các mảng Numpy một chiều nhưng có thêm một thuộc tính là labels. Series có thể được tạo ra từ một giá trị vô hướng _(scalar)_, một list, một mảng numpy hoặc một dictionary sử dụng hàm `pd.Series()`.

### 1.1. Tạo series

Chúng ta bắt đầu tạo một series đơn giản từ list. Theo mặc định các labels và index bắt đầu từ `0`.



```python
pd.Series(data = [-5, 1.3, 21, 6, 3])
```




    0    -5.0
    1     1.3
    2    21.0
    3     6.0
    4     3.0
    dtype: float64



Chúng ta có thể gán nhãn _(labels)_ cụ thể cho các giá trị thay vì sử dụng index:


```python
pd.Series(data = [-5, 1.3, 21, 6, 3],
          index = ['a', 'b', 'c', 'd', 'e'])
```




    a    -5.0
    b     1.3
    c    21.0
    d     6.0
    e     3.0
    dtype: float64



Tạo một series từ dictionary:


```python
pd.Series(data = {'a': 10, 'b': 20, 'c': 30})
```




    a    10
    b    20
    c    30
    dtype: int64



Tạo một series từ mảng numpy:


```python
pd.Series(data = np.random.randn(3))
```




    0    0.103119
    1   -1.431701
    2   -0.745353
    dtype: float64



Tạo series từ scalar:


```python
pd.Series(3.141)
```




    0    3.141
    dtype: float64




```python
pd.Series(data=3.141, index=['a', 'b', 'c'])
```




    a    3.141
    b    3.141
    c    3.141
    dtype: float64



### 1.2. Thuộc tính

Hai thuộc tính quan trọng nhất của series là _index_ và _array_:

- **index**: Mảng các chỉ số hoặc labels của series.
- **array**: Mảng chứa các dữ liệu trong series.

Ví dụ:


```python
s = pd.Series(data = np.random.randn(5))
s.index
```




    RangeIndex(start=0, stop=5, step=1)




```python
s.array
```




    <PandasArray>
    [  0.6727783719149419,   -0.182362859573495, -0.17737350985083752,
       1.0327929875759876,   -0.813223486205808]
    Length: 5, dtype: float64




```python
s.to_numpy()
```




    array([ 0.67277837, -0.18236286, -0.17737351,  1.03279299, -0.81322349])



### 1.3. Indexing và slicing

Giả sử ta có một series như sau:


```python
s = pd.Series(data = range(5),
              index = ['A', 'B', 'C', 'D', 'E'])
s
```




    A    0
    B    1
    C    2
    D    3
    E    4
    dtype: int64



Chúng ta có thể lấy ra các phần tử sử dụng index là các chỉ số chỉ vị trí tương tự như trong list, array.


```python
# Lấy ra một phần tử
s[0]
```




    0




```python
# Lấy ra nhiều phần tử
s[[1, 3, 2]]
```




    B    1
    D    3
    C    2
    dtype: int64




```python
# Slicing
s[0:3]
```




    A    0
    B    1
    C    2
    dtype: int64



Series tương tự như dictionary, ta cũng có thể lấy các phần tử dựa vào labels.


```python
# Lấy ra một phần tử
s["A"]
```




    0




```python
# Lấy ra nhiều phần tử
s[["B", "D", "C"]]
```




    B    1
    D    3
    C    2
    dtype: int64




```python
# Kiểm tra xem một labels có trong series hay không
"A" in s
```




    True



Lưu ý khi sử dụng labels, nếu các labels không phải là duy nhất:


```python
x = pd.Series(data = range(5),
              index = ["A", "A", "A", "B", "C"])
x["A"]
```




    A    0
    A    1
    A    2
    dtype: int64



Tương tự như numpy, chúng ta cũng có thể sử dụng _boolean mask_ để lấy ra các phần tử thỏa mãn một điều kiện nào đó.


```python
idx = (s > 1)
idx
```




    A    False
    B    False
    C     True
    D     True
    E     True
    dtype: bool




```python
s[idx]
```




    C    2
    D    3
    E    4
    dtype: int64



### 1.4. Toán tử

Không như mảng numpy, các toán tử `+, -, *, /` giữa hai series sẽ dựa vào labels của các phần tử mà không phải là vị trí của nó:

{{< figure src="./series_addition.png" >}}

Ví dụ:


```python
s1 = pd.Series(data = range(4),
               index = ["A", "B", "C", "D"])
s1
```




    A    0
    B    1
    C    2
    D    3
    dtype: int64




```python
s2 = pd.Series(data = range(10, 14),
               index = ["B", "C", "D", "E"])
s2
```




    B    10
    C    11
    D    12
    E    13
    dtype: int64




```python
s1 + s2
```




    A     NaN
    B    11.0
    C    13.0
    D    15.0
    E     NaN
    dtype: float64



Như bạn có thể thấy vì `A` và `E` bị thiếu giá trị cho nên kết quả trả về là `NaN`

### 1.5. Missing value

Chúng ta sử dụng `np.nan` để đại diện cho missing value.


```python
s3 = pd.Series([1, 2, 3, np.nan])
s3
```




    0    1.0
    1    2.0
    2    3.0
    3    NaN
    dtype: float64




```python
# Kiểm tra giá trị missing
s3.isnull()
```




    0    False
    1    False
    2    False
    3     True
    dtype: bool




```python
# Kiểm tra các giá trị không missing
pd.notnull(s3)
```




    0     True
    1     True
    2     True
    3    False
    dtype: bool



## 2. DataFrames

{{< figure src="./dataframe.png" >}}

Có nhiều cách để nghĩ về DataFrames. Bạn có thể nghĩ DataFrames giống như các bảng dữ liệu trong Excel hoặc database. Nó cũng gần giống với một dictionary với key là tên biến, cột, còn giá trị là một series.

### 2.1. Tạo DataFrames

Cú pháp tổng quát:

```python
# array_2d: Là mảng dữ liệu 2 chiều của các giá trị
# index là list các labels 
# columns là danh sách tên cột, biến
pd.DataFrame(array_2d, index, columns)

# Dictionary với key là tên biến, values là list các giá trị
pd.DataFrame(dictionary, index)
```

Ví dụ:

```python
# lists of lists
pd.DataFrame([['Tom', 7], 
              ['Mike', 15], 
              ['Tiffany', 3]
              ])

# array	
pd.DataFrame(np.array([['Tom', 7], 
                       ['Mike', 15], 
                       ['Tiffany', 3]
                       ]))

# dictionary
pd.DataFrame({"Name": ['Tom', 'Mike', 'Tiffany'], 
              "Number": [7, 15, 3]})

# Series	
pd.DataFrame({"Name": pd.Series(['Tom', 'Mike', 'Tiffany']), 
              "Number": pd.Series([7, 15, 3])})

# list of tuples
pd.DataFrame(zip(['Tom', 'Mike', 'Tiffany'], 
                 [7, 15, 3]
                 ))
```



### 2.2. Indexing và slicing

Chúng ta có 5 cách để lấy ra các phần tử từ trong DataFrame:

- Sử dụng `[]`
- Sử dụng `.loc[]` với index là các labels.
- Sử dụng `.iloc[]` với index là các chỉ số chỉ vị trí.
- Sử dụng _boolean mask_.
- Sử dụng `.query()`

Chúng ta có một DataFrame đơn giản như sau:


```python
df = pd.DataFrame({"Name": ["Tom", "Mike", "Tiffany"],
                   "Language": ["Python", "Python", "R"],
                   "Courses": [5, 4, 7]})
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Language</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>Python</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
      <td>Python</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
      <td>R</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



**Lọc các cột với `[]`:**


```python
# Lấy ra một cột
# Trả về một series
df['Name']
```




    0        Tom
    1       Mike
    2    Tiffany
    Name: Name, dtype: object




```python
# Lấy ra một tập hợp các cột, trả về một df
df[['Name']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[['Name', 'Courses']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



**Lọc các quan sát và các cột với `.loc` và `.iloc`:**


```python
# Lấy ra một hàng, sẽ trả về một series
df.iloc[0]
```




    Name           Tom
    Language    Python
    Courses          5
    Name: 0, dtype: object




```python
# Lấy ra một tập hợp các hàng, trả về dataframe
df.iloc[0:3]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Language</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>Python</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
      <td>Python</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
      <td>R</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Lọc các quan sát và các cột
df.iloc[0:2, [1, 2]]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Language</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Python</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Python</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Lọc các quan sát sử dụng label
df.loc[:, ['Name']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
    </tr>
  </tbody>
</table>
</div>



Đôi khi, chúng ta sẽ phải sử dụng kết hợp giữa các labels với các chỉ số chỉ vị trí:


```python
print(df.index)
print(df.columns)
```

    RangeIndex(start=0, stop=3, step=1)
    Index(['Name', 'Language', 'Courses'], dtype='object')
    


```python
df.loc[df.index[0], 'Courses']
```




    5




```python
df.loc[2, df.columns[1]]
```




    'R'



**Lọc các quan sát với boolean mask:**


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Language</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>Python</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
      <td>Python</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
      <td>R</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['Courses'] > 5
```




    0    False
    1    False
    2     True
    Name: Courses, dtype: bool




```python
df[df['Courses'] > 5]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Language</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
      <td>R</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[df['Name'] == "Tom"]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Language</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>Python</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



**Lọc các quan sát với `.query()`**

Tương tự như _boolean masks_, nhưng chỉ khác nhau về mặt cú pháp.


```python
df.query("Courses > 4 & Language == 'Python'")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Language</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>Python</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Chúng ta có thể sử dụng tham số với @variable
course_threshold = 4
df.query("Courses > @course_threshold")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Language</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>Python</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
      <td>R</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



Tổng kết, chúng ta có những trường hợp sau:

```python
# Select column, return series
df['Column_name']

# Select row slice
df[row_1_int:row_2_int]

# Select row/columns by labels
df.loc[row_label(s), col_label(s)]

# Select row/columns by index
df.iloc[row_int(s), col_int(s)]

# Select row by index, column by labels
df.loc[df.index[row_int], col_label]

# Select row by labels, columb by index
df.loc[row_label, df.columns[col_int]]

# Select by boolean expression
df.query("expression")

# query with parameter
df.query("Courses > @course_threshold")
```

### 2.3. Import CSV file

Cú pháp:

```python
# path: đường dẫn đến file, có thể là url
# index_col: Chỉ định cột làm index
# header, skiprows
# parse_dates = True: Cố gắng xác định các cột có kiểu datetime
pd.read_csv(path, index_col, parse_dates, )
```

Ví dụ:


```python
df = pd.read_csv('./cycling_data.csv', parse_dates = True)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>5</th>
      <td>16 Sep 2019, 13:57:48</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2272</td>
      <td>12.45</td>
      <td>Rested after the weekend!</td>
    </tr>
    <tr>
      <th>6</th>
      <td>17 Sep 2019, 00:15:47</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1973</td>
      <td>12.45</td>
      <td>Legs feeling strong!</td>
    </tr>
    <tr>
      <th>7</th>
      <td>17 Sep 2019, 13:43:34</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2285</td>
      <td>12.60</td>
      <td>Raining</td>
    </tr>
    <tr>
      <th>8</th>
      <td>18 Sep 2019, 13:49:53</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2903</td>
      <td>14.57</td>
      <td>Raining today</td>
    </tr>
    <tr>
      <th>9</th>
      <td>18 Sep 2019, 00:15:52</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2101</td>
      <td>12.48</td>
      <td>Pumped up tires</td>
    </tr>
    <tr>
      <th>10</th>
      <td>19 Sep 2019, 00:30:01</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>48062</td>
      <td>12.48</td>
      <td>Feeling good</td>
    </tr>
    <tr>
      <th>11</th>
      <td>19 Sep 2019, 13:52:09</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2090</td>
      <td>12.59</td>
      <td>Getting colder which is nice</td>
    </tr>
    <tr>
      <th>12</th>
      <td>20 Sep 2019, 01:02:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2961</td>
      <td>12.81</td>
      <td>Feeling good</td>
    </tr>
    <tr>
      <th>13</th>
      <td>23 Sep 2019, 13:50:41</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2462</td>
      <td>12.68</td>
      <td>Rested after the weekend!</td>
    </tr>
    <tr>
      <th>14</th>
      <td>24 Sep 2019, 00:35:42</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2076</td>
      <td>12.47</td>
      <td>Oiled chain, bike feels smooth</td>
    </tr>
    <tr>
      <th>15</th>
      <td>24 Sep 2019, 13:41:24</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2321</td>
      <td>12.68</td>
      <td>Bike feeling much smoother</td>
    </tr>
    <tr>
      <th>16</th>
      <td>25 Sep 2019, 00:07:21</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1775</td>
      <td>12.10</td>
      <td>Feeling really tired</td>
    </tr>
    <tr>
      <th>17</th>
      <td>25 Sep 2019, 13:35:41</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2124</td>
      <td>12.65</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>18</th>
      <td>26 Sep 2019, 00:13:33</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1860</td>
      <td>12.52</td>
      <td>raining</td>
    </tr>
    <tr>
      <th>19</th>
      <td>26 Sep 2019, 13:42:43</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2350</td>
      <td>12.91</td>
      <td>Detour around trucks at Jericho</td>
    </tr>
    <tr>
      <th>20</th>
      <td>27 Sep 2019, 01:00:18</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1712</td>
      <td>12.47</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>21</th>
      <td>30 Sep 2019, 13:53:52</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2118</td>
      <td>12.71</td>
      <td>Rested after the weekend!</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1 Oct 2019, 00:15:07</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1732</td>
      <td>NaN</td>
      <td>Legs feeling strong!</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1 Oct 2019, 13:45:55</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2222</td>
      <td>12.82</td>
      <td>Beautiful morning! Feeling fit</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2 Oct 2019, 00:13:09</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1756</td>
      <td>NaN</td>
      <td>A little tired today but good weather</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2 Oct 2019, 13:46:06</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2134</td>
      <td>13.06</td>
      <td>Bit tired today but good weather</td>
    </tr>
    <tr>
      <th>26</th>
      <td>3 Oct 2019, 00:45:22</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1724</td>
      <td>12.52</td>
      <td>Feeling good</td>
    </tr>
    <tr>
      <th>27</th>
      <td>3 Oct 2019, 13:47:36</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2182</td>
      <td>12.68</td>
      <td>Wet road</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
  </tbody>
</table>
</div>



### 2.4. Các toán tử

DataFrames có nhiều hàm được xây dựng sẵn phục vụ cho các mục đích phân tích và xử lý dữ liệu.

Một số ví dụ:


```python
df.sum()
```




    Date        10 Sep 2019, 00:13:0410 Sep 2019, 13:52:1811 S...
    Name        Afternoon RideMorning RideAfternoon RideMornin...
    Type        RideRideRideRideRideRideRideRideRideRideRideRi...
    Time                                                   115922
    Distance                                               392.69
    Comments    RainrainWet road but nice weatherStopped for p...
    dtype: object




```python
df.min()
```




    Date                         1 Oct 2019, 00:15:07
    Name                               Afternoon Ride
    Type                                         Ride
    Time                                         1712
    Distance                                    11.79
    Comments    A little tired today but good weather
    dtype: object




```python
df['Time'].min()
```




    1712




```python
df['Time'].idxmin()
```




    20




```python
df.loc[20]
```




    Date               27 Sep 2019, 01:00:18
    Name                      Afternoon Ride
    Type                                Ride
    Time                                1712
    Distance                           12.47
    Comments    Tired by the end of the week
    Name: 20, dtype: object




```python
# Sắp xếp theo value
# ascending = True
df.sort_values(by = 'Time')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>27 Sep 2019, 01:00:18</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1712</td>
      <td>12.47</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>26</th>
      <td>3 Oct 2019, 00:45:22</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1724</td>
      <td>12.52</td>
      <td>Feeling good</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1 Oct 2019, 00:15:07</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1732</td>
      <td>NaN</td>
      <td>Legs feeling strong!</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2 Oct 2019, 00:13:09</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1756</td>
      <td>NaN</td>
      <td>A little tired today but good weather</td>
    </tr>
    <tr>
      <th>16</th>
      <td>25 Sep 2019, 00:07:21</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1775</td>
      <td>12.10</td>
      <td>Feeling really tired</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
    <tr>
      <th>18</th>
      <td>26 Sep 2019, 00:13:33</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1860</td>
      <td>12.52</td>
      <td>raining</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>6</th>
      <td>17 Sep 2019, 00:15:47</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1973</td>
      <td>12.45</td>
      <td>Legs feeling strong!</td>
    </tr>
    <tr>
      <th>14</th>
      <td>24 Sep 2019, 00:35:42</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2076</td>
      <td>12.47</td>
      <td>Oiled chain, bike feels smooth</td>
    </tr>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>11</th>
      <td>19 Sep 2019, 13:52:09</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2090</td>
      <td>12.59</td>
      <td>Getting colder which is nice</td>
    </tr>
    <tr>
      <th>9</th>
      <td>18 Sep 2019, 00:15:52</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2101</td>
      <td>12.48</td>
      <td>Pumped up tires</td>
    </tr>
    <tr>
      <th>21</th>
      <td>30 Sep 2019, 13:53:52</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2118</td>
      <td>12.71</td>
      <td>Rested after the weekend!</td>
    </tr>
    <tr>
      <th>17</th>
      <td>25 Sep 2019, 13:35:41</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2124</td>
      <td>12.65</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2 Oct 2019, 13:46:06</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2134</td>
      <td>13.06</td>
      <td>Bit tired today but good weather</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>27</th>
      <td>3 Oct 2019, 13:47:36</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2182</td>
      <td>12.68</td>
      <td>Wet road</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1 Oct 2019, 13:45:55</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2222</td>
      <td>12.82</td>
      <td>Beautiful morning! Feeling fit</td>
    </tr>
    <tr>
      <th>5</th>
      <td>16 Sep 2019, 13:57:48</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2272</td>
      <td>12.45</td>
      <td>Rested after the weekend!</td>
    </tr>
    <tr>
      <th>7</th>
      <td>17 Sep 2019, 13:43:34</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2285</td>
      <td>12.60</td>
      <td>Raining</td>
    </tr>
    <tr>
      <th>15</th>
      <td>24 Sep 2019, 13:41:24</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2321</td>
      <td>12.68</td>
      <td>Bike feeling much smoother</td>
    </tr>
    <tr>
      <th>19</th>
      <td>26 Sep 2019, 13:42:43</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2350</td>
      <td>12.91</td>
      <td>Detour around trucks at Jericho</td>
    </tr>
    <tr>
      <th>13</th>
      <td>23 Sep 2019, 13:50:41</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2462</td>
      <td>12.68</td>
      <td>Rested after the weekend!</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>8</th>
      <td>18 Sep 2019, 13:49:53</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2903</td>
      <td>14.57</td>
      <td>Raining today</td>
    </tr>
    <tr>
      <th>12</th>
      <td>20 Sep 2019, 01:02:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2961</td>
      <td>12.81</td>
      <td>Feeling good</td>
    </tr>
    <tr>
      <th>10</th>
      <td>19 Sep 2019, 00:30:01</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>48062</td>
      <td>12.48</td>
      <td>Feeling good</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sort by index
df.sort_index(ascending = False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>27</th>
      <td>3 Oct 2019, 13:47:36</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2182</td>
      <td>12.68</td>
      <td>Wet road</td>
    </tr>
    <tr>
      <th>26</th>
      <td>3 Oct 2019, 00:45:22</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1724</td>
      <td>12.52</td>
      <td>Feeling good</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2 Oct 2019, 13:46:06</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2134</td>
      <td>13.06</td>
      <td>Bit tired today but good weather</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2 Oct 2019, 00:13:09</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1756</td>
      <td>NaN</td>
      <td>A little tired today but good weather</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1 Oct 2019, 13:45:55</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2222</td>
      <td>12.82</td>
      <td>Beautiful morning! Feeling fit</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1 Oct 2019, 00:15:07</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1732</td>
      <td>NaN</td>
      <td>Legs feeling strong!</td>
    </tr>
    <tr>
      <th>21</th>
      <td>30 Sep 2019, 13:53:52</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2118</td>
      <td>12.71</td>
      <td>Rested after the weekend!</td>
    </tr>
    <tr>
      <th>20</th>
      <td>27 Sep 2019, 01:00:18</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1712</td>
      <td>12.47</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>19</th>
      <td>26 Sep 2019, 13:42:43</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2350</td>
      <td>12.91</td>
      <td>Detour around trucks at Jericho</td>
    </tr>
    <tr>
      <th>18</th>
      <td>26 Sep 2019, 00:13:33</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1860</td>
      <td>12.52</td>
      <td>raining</td>
    </tr>
    <tr>
      <th>17</th>
      <td>25 Sep 2019, 13:35:41</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2124</td>
      <td>12.65</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>16</th>
      <td>25 Sep 2019, 00:07:21</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1775</td>
      <td>12.10</td>
      <td>Feeling really tired</td>
    </tr>
    <tr>
      <th>15</th>
      <td>24 Sep 2019, 13:41:24</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2321</td>
      <td>12.68</td>
      <td>Bike feeling much smoother</td>
    </tr>
    <tr>
      <th>14</th>
      <td>24 Sep 2019, 00:35:42</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2076</td>
      <td>12.47</td>
      <td>Oiled chain, bike feels smooth</td>
    </tr>
    <tr>
      <th>13</th>
      <td>23 Sep 2019, 13:50:41</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2462</td>
      <td>12.68</td>
      <td>Rested after the weekend!</td>
    </tr>
    <tr>
      <th>12</th>
      <td>20 Sep 2019, 01:02:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2961</td>
      <td>12.81</td>
      <td>Feeling good</td>
    </tr>
    <tr>
      <th>11</th>
      <td>19 Sep 2019, 13:52:09</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2090</td>
      <td>12.59</td>
      <td>Getting colder which is nice</td>
    </tr>
    <tr>
      <th>10</th>
      <td>19 Sep 2019, 00:30:01</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>48062</td>
      <td>12.48</td>
      <td>Feeling good</td>
    </tr>
    <tr>
      <th>9</th>
      <td>18 Sep 2019, 00:15:52</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2101</td>
      <td>12.48</td>
      <td>Pumped up tires</td>
    </tr>
    <tr>
      <th>8</th>
      <td>18 Sep 2019, 13:49:53</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2903</td>
      <td>14.57</td>
      <td>Raining today</td>
    </tr>
    <tr>
      <th>7</th>
      <td>17 Sep 2019, 13:43:34</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2285</td>
      <td>12.60</td>
      <td>Raining</td>
    </tr>
    <tr>
      <th>6</th>
      <td>17 Sep 2019, 00:15:47</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1973</td>
      <td>12.45</td>
      <td>Legs feeling strong!</td>
    </tr>
    <tr>
      <th>5</th>
      <td>16 Sep 2019, 13:57:48</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2272</td>
      <td>12.45</td>
      <td>Rested after the weekend!</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
  </tbody>
</table>
</div>



## 3. View DataFrames

Xem n hàng đầu tiên hoặc cuối cùng của DataFrame


```python
# Lấy 5 hàng đầu tiên
df.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Lấy 5 hàng cuối cùng
df.tail(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
  </tbody>
</table>
</div>



Một số thuộc tính của DataFrame:

- `.shape`: Tương tự như shape của mảng numpy.
- `.info()`: Xem một số thông tin về kiểu dữ liệu của từng cột, biến.
- `.describe()`: Một số thông tin thống kê mô tả cơ bản


```python
df.shape
```




    (33, 6)




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 33 entries, 0 to 32
    Data columns (total 6 columns):
     #   Column    Non-Null Count  Dtype  
    ---  ------    --------------  -----  
     0   Date      33 non-null     object 
     1   Name      33 non-null     object 
     2   Type      33 non-null     object 
     3   Time      33 non-null     int64  
     4   Distance  31 non-null     float64
     5   Comments  33 non-null     object 
    dtypes: float64(1), int64(1), object(4)
    memory usage: 1.7+ KB
    


```python
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Time</th>
      <th>Distance</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>33.000000</td>
      <td>31.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>3512.787879</td>
      <td>12.667419</td>
    </tr>
    <tr>
      <th>std</th>
      <td>8003.309233</td>
      <td>0.428618</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1712.000000</td>
      <td>11.790000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1863.000000</td>
      <td>12.480000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2118.000000</td>
      <td>12.620000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2285.000000</td>
      <td>12.750000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>48062.000000</td>
      <td>14.570000</td>
    </tr>
  </tbody>
</table>
</div>



Theo mặc định thì, nếu DataFrame có nhiều hơn 60 dòng, Pandas sẽ hiển thị 5 dòng đầu tiên và 5 dòng cuối cùng của DataFrame, ngược lại nó sẽ hiển thị tất cả các dòng. Bạn cũng có thể sử dụng tùy chọn sau để thay đổi `60` thành một con số bất kỳ mà bạn muốn.


```python
# n = 20
pd.set_option("display.max_rows", 20)
```

## 4. Data manipulation

### 4.1. Đổi tên cột

Có hai cách để đổi tên cột bằng Pandas:

- Đổi tên một hoặc một số cột với `df.rename()`
- Đổi tên tất cả các cột với `df.columns()`


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 6 columns</p>
</div>




```python
df.rename(columns = {"Date": "Datetime",
                     "Comments": "Notes"}
         )
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 6 columns</p>
</div>



Ôi chuyện gì đã xảy ra vậy, rõ ràng chúng ta đã đổi tên các cột nhưng trên thực tế nó không thay đổi. Phương thức `df.rename()` tạo ra một bản sao mới. Do đó ta phải gán lại nó cho `df`.


```python
df = df.rename(columns={"Date": "Datetime",
                   "Comments": "Notes"})
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Datetime</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 6 columns</p>
</div>



### 4.2. Thay đổi index

Chúng ta có một số cách thay đổi index của DataFrame:

- `df.set_index()`: Chỉ định một cột làm index
- `df.index.name`: Đổi tên index
- `df.reset_index()`: Chuyển index hiện tại thành một cột 
- `df.index`: Thay đổi index thông qua thuộc tính



```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Datetime</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 6 columns</p>
</div>




```python
# df.set_index sẽ tạo ra một copy
df = df.set_index('Datetime')
df.index.name = "Date Index"
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Notes</th>
    </tr>
    <tr>
      <th>Date Index</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10 Sep 2019, 00:13:04</th>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>10 Sep 2019, 13:52:18</th>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>11 Sep 2019, 00:23:50</th>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>11 Sep 2019, 14:06:19</th>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>12 Sep 2019, 00:28:05</th>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4 Oct 2019, 01:08:08</th>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>9 Oct 2019, 13:55:40</th>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>10 Oct 2019, 00:10:31</th>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>10 Oct 2019, 13:47:14</th>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>11 Oct 2019, 00:16:57</th>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 5 columns</p>
</div>




```python
df = df.reset_index()
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date Index</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 6 columns</p>
</div>



### 4.3. Thêm hoặc xóa cột

Chúng ta có thể thêm hoặc xóa columns với:

- Sử dụng `df['variable_name']` để thêm một cột mới 
- Sử dụng `df.drop()` để xóa các cột


```python
df['Rider'] = 'Tom Beuzen'
df['Avg Speed'] = df['Distance'] * 1000 / df['Time']  # avg. speed in m/s
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date Index</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Notes</th>
      <th>Rider</th>
      <th>Avg Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
      <td>Tom Beuzen</td>
      <td>6.055662</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
      <td>Tom Beuzen</td>
      <td>5.148163</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
      <td>Tom Beuzen</td>
      <td>6.720344</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
      <td>Tom Beuzen</td>
      <td>5.857664</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
      <td>Tom Beuzen</td>
      <td>6.599683</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
      <td>Tom Beuzen</td>
      <td>6.754011</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
      <td>Tom Beuzen</td>
      <td>5.909725</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
      <td>Tom Beuzen</td>
      <td>6.838675</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
      <td>Tom Beuzen</td>
      <td>5.192854</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
      <td>Tom Beuzen</td>
      <td>6.397179</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 8 columns</p>
</div>




```python
df = df.drop(columns = ['Rider', 'Avg Speed'])
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date Index</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 6 columns</p>
</div>



### 4.4. Thêm hoặc xóa hàng

Tương tự như với cột chúng ta cũng có hai cách để thêm hoặc xóa hàng:

- Thêm các hàng với `df.append()`
- Xóa các hàng với `df.drop()`


```python
another_row = pd.DataFrame([["12 Oct 2019, 00:10:57", "Morning Ride", "Ride",
                             2331, 12.67, "Washed and oiled bike last night"]],
                           columns = df.columns,
                           index = [33])
df = df.append(another_row)
df
```

    C:\Users\ktuyends\AppData\Local\Temp/ipykernel_5224/1774859891.py:5: FutureWarning: The frame.append method is deprecated and will be removed from pandas in a future version. Use pandas.concat instead.
      df = df.append(another_row)
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date Index</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10 Oct 2019, 00:10:31</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1841</td>
      <td>12.59</td>
      <td>Feeling good after a holiday break!</td>
    </tr>
    <tr>
      <th>31</th>
      <td>10 Oct 2019, 13:47:14</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2463</td>
      <td>12.79</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>32</th>
      <td>11 Oct 2019, 00:16:57</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1843</td>
      <td>11.79</td>
      <td>Bike feeling tight, needs an oil and pump</td>
    </tr>
    <tr>
      <th>33</th>
      <td>12 Oct 2019, 00:10:57</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2331</td>
      <td>12.67</td>
      <td>Washed and oiled bike last night</td>
    </tr>
  </tbody>
</table>
<p>34 rows × 6 columns</p>
</div>




```python
df.drop(index = range(30, 34))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date Index</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10 Sep 2019, 00:13:04</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>2084</td>
      <td>12.62</td>
      <td>Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10 Sep 2019, 13:52:18</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2531</td>
      <td>13.03</td>
      <td>rain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11 Sep 2019, 00:23:50</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1863</td>
      <td>12.52</td>
      <td>Wet road but nice weather</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11 Sep 2019, 14:06:19</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2192</td>
      <td>12.84</td>
      <td>Stopped for photo of sunrise</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12 Sep 2019, 00:28:05</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1891</td>
      <td>12.48</td>
      <td>Tired by the end of the week</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2 Oct 2019, 13:46:06</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2134</td>
      <td>13.06</td>
      <td>Bit tired today but good weather</td>
    </tr>
    <tr>
      <th>26</th>
      <td>3 Oct 2019, 00:45:22</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1724</td>
      <td>12.52</td>
      <td>Feeling good</td>
    </tr>
    <tr>
      <th>27</th>
      <td>3 Oct 2019, 13:47:36</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2182</td>
      <td>12.68</td>
      <td>Wet road</td>
    </tr>
    <tr>
      <th>28</th>
      <td>4 Oct 2019, 01:08:08</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>1870</td>
      <td>12.63</td>
      <td>Very tired, riding into the wind</td>
    </tr>
    <tr>
      <th>29</th>
      <td>9 Oct 2019, 13:55:40</td>
      <td>Morning Ride</td>
      <td>Ride</td>
      <td>2149</td>
      <td>12.70</td>
      <td>Really cold! But feeling good</td>
    </tr>
  </tbody>
</table>
<p>30 rows × 6 columns</p>
</div>



### 4.5. Sửa đổi giá trị

Khi muốn sửa đổi một giá trị bên trong DataFrame ta nên sử dụng `.loc` hoặc `.iloc`, vì sử dụng `[]` sẽ tạo ra một bản copy. Ví dụ:


```python
df[df['Time'] > 4000]['Time'] = 2000
```

    C:\Users\ktuyends\AppData\Local\Temp/ipykernel_5224/808031618.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      df[df['Time'] > 4000]['Time'] = 2000
    


```python
df[df['Time'] > 4000]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date Index</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>19 Sep 2019, 00:30:01</td>
      <td>Afternoon Ride</td>
      <td>Ride</td>
      <td>48062</td>
      <td>12.48</td>
      <td>Feeling good</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[df['Time'] > 4000, 'Time'] = 2000
df[df['Time'] > 4000]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date Index</th>
      <th>Name</th>
      <th>Type</th>
      <th>Time</th>
      <th>Distance</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



## 5. Data reshaping

Chúng ta có 3 cách để biển đổi cấu trúc một DataFrame:

- `df.melt()`: Chuyển dữ liệu từ dạng wide về long.
- `df.pivot()`: Chuyển dữ liệu từ dạng long về wide.
- `df.pivot_table()`: Tương tự như pivot, nhưng xử lý được nhiều index hơn.

### 5.1. Melt và pivot

Giả sử ta có một DataFrame như sau:


```python
df = pd.DataFrame({"Name": ["Tom", "Mike", "Tiffany", "Varada", "Joel"],
                   "2018": [1, 3, 4, 5, 3],
                   "2019": [2, 4, 3, 2, 1],
                   "2020": [5, 2, 4, 4, 3]})
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>2018</th>
      <th>2019</th>
      <th>2020</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>1</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
      <td>3</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
      <td>4</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Varada</td>
      <td>5</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Joel</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_long = df.melt(id_vars = "Name",
                  var_name = "Year",
                  value_name = "Courses")
df_long
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Year</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>2018</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
      <td>2018</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
      <td>2018</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Varada</td>
      <td>2018</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Joel</td>
      <td>2018</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Tom</td>
      <td>2019</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Mike</td>
      <td>2019</td>
      <td>4</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Tiffany</td>
      <td>2019</td>
      <td>3</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Varada</td>
      <td>2019</td>
      <td>2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Joel</td>
      <td>2019</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Tom</td>
      <td>2020</td>
      <td>5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Mike</td>
      <td>2020</td>
      <td>2</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Tiffany</td>
      <td>2020</td>
      <td>4</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Varada</td>
      <td>2020</td>
      <td>4</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Joel</td>
      <td>2020</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.melt(id_vars = "Name",
        value_vars = ["2019", "2020"],
        var_name = "Year",
        value_name = "Courses")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Year</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>2019</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
      <td>2019</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
      <td>2019</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Varada</td>
      <td>2019</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Joel</td>
      <td>2019</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Tom</td>
      <td>2020</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Mike</td>
      <td>2020</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Tiffany</td>
      <td>2020</td>
      <td>4</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Varada</td>
      <td>2020</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Joel</td>
      <td>2020</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_wide = df_long.pivot(index = "Name",
                        columns = "Year",
                        values = "Courses")
df_wide = df_wide.reset_index()
df_wide.columns.name = None
df_wide
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>2018</th>
      <th>2019</th>
      <th>2020</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Joel</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mike</td>
      <td>3</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tiffany</td>
      <td>4</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Tom</td>
      <td>1</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Varada</td>
      <td>5</td>
      <td>2</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



### 5.2. Pivot table


```python
# Trường hợp có nhiều cột index
df = pd.DataFrame({"Name": ["Tom", "Tom", "Mike", "Mike"],
                   "Department": ["CS", "STATS", "CS", "STATS"],
                   "2018": [1, 2, 3, 1],
                   "2019": [2, 3, 4, 2],
                   "2020": [5, 1, 2, 2]})
df                   
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Department</th>
      <th>2018</th>
      <th>2019</th>
      <th>2020</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>CS</td>
      <td>1</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Tom</td>
      <td>STATS</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mike</td>
      <td>CS</td>
      <td>3</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mike</td>
      <td>STATS</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
df = df.melt(id_vars = ['Name', 'Department'],
             value_name = 'Courses',
             var_name = 'Year')
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Department</th>
      <th>Year</th>
      <th>Courses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Tom</td>
      <td>CS</td>
      <td>2018</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Tom</td>
      <td>STATS</td>
      <td>2018</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mike</td>
      <td>CS</td>
      <td>2018</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mike</td>
      <td>STATS</td>
      <td>2018</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Tom</td>
      <td>CS</td>
      <td>2019</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Tom</td>
      <td>STATS</td>
      <td>2019</td>
      <td>3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Mike</td>
      <td>CS</td>
      <td>2019</td>
      <td>4</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Mike</td>
      <td>STATS</td>
      <td>2019</td>
      <td>2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Tom</td>
      <td>CS</td>
      <td>2020</td>
      <td>5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Tom</td>
      <td>STATS</td>
      <td>2020</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Mike</td>
      <td>CS</td>
      <td>2020</td>
      <td>2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Mike</td>
      <td>STATS</td>
      <td>2020</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_table(index = "Name", 
               columns='Year', 
               values='Courses', 
               aggfunc='sum')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Year</th>
      <th>2018</th>
      <th>2019</th>
      <th>2020</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mike</th>
      <td>4</td>
      <td>6</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Tom</th>
      <td>3</td>
      <td>5</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.pivot_table(index = ["Name", "Department"], 
               columns='Year', 
               values='Courses', 
               aggfunc='sum')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>2018</th>
      <th>2019</th>
      <th>2020</th>
    </tr>
    <tr>
      <th>Name</th>
      <th>Department</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Mike</th>
      <th>CS</th>
      <td>3</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>STATS</th>
      <td>1</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Tom</th>
      <th>CS</th>
      <td>1</td>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>STATS</th>
      <td>2</td>
      <td>3</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



## 6. Merge and Concat

### 6.1. Concat

Đôi khi chúng ta sẽ phải làm việc giữa nhiều DataFrame, và việc kết hợp giữa các DataFrame với nhau là một trong những việc chúng ta phải làm.




```python
df1 = pd.DataFrame({'A': [1, 3, 5],
                    'B': [2, 4, 6]})
df2 = pd.DataFrame({'A': [7, 9, 11],
                    'B': [8, 10, 12]})
df1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Kết hợp 2 dataframe theo chiều dọc
pd.concat((df1, df2), axis = 0, ignore_index=True)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>5</th>
      <td>11</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Đổi tên columns
df2.columns = ['C', 'D']

# Kết hợp 2 dataframe theo chiều ngang
pd.concat((df1, df2), axis = 1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>7</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>4</td>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>6</td>
      <td>11</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



### 6.2. Merge

Chúng ta có thể nghĩ merge hai DataFrame tương tự như phép JOIN 2 bảng trong SQL vậy. Giả sử ta có hai bảng như sau:

{{< figure src="./merge.png" >}}


```python
df1 = pd.DataFrame({"name": ['Magneto', 'Storm', 'Mystique', 'Batman', 'Joker', 'Catwoman', 'Hellboy'],
                    'alignment': ['bad', 'good', 'bad', 'good', 'bad', 'bad', 'good'],
                    'gender': ['male', 'female', 'female', 'male', 'male', 'female', 'male'],
                    'publisher': ['Marvel', 'Marvel', 'Marvel', 'DC', 'DC', 'DC', 'Dark Horse Comics']})
df2 = pd.DataFrame({'publisher': ['DC', 'Marvel', 'Image'],
                    'year_founded': [1934, 1939, 1992]})
```



**Inner Join**

{{< figure src="./inner_join.png" >}}


```python
pd.merge(df1, df2, how = "inner", on = "publisher")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>alignment</th>
      <th>gender</th>
      <th>publisher</th>
      <th>year_founded</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Magneto</td>
      <td>bad</td>
      <td>male</td>
      <td>Marvel</td>
      <td>1939</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Storm</td>
      <td>good</td>
      <td>female</td>
      <td>Marvel</td>
      <td>1939</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mystique</td>
      <td>bad</td>
      <td>female</td>
      <td>Marvel</td>
      <td>1939</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Batman</td>
      <td>good</td>
      <td>male</td>
      <td>DC</td>
      <td>1934</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Joker</td>
      <td>bad</td>
      <td>male</td>
      <td>DC</td>
      <td>1934</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Catwoman</td>
      <td>bad</td>
      <td>female</td>
      <td>DC</td>
      <td>1934</td>
    </tr>
  </tbody>
</table>
</div>



**Outer Join**

{{< figure src="./outer_join.png" >}}


```python
pd.merge(df1, df2, how = "outer", on = "publisher")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>alignment</th>
      <th>gender</th>
      <th>publisher</th>
      <th>year_founded</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Magneto</td>
      <td>bad</td>
      <td>male</td>
      <td>Marvel</td>
      <td>1939.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Storm</td>
      <td>good</td>
      <td>female</td>
      <td>Marvel</td>
      <td>1939.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mystique</td>
      <td>bad</td>
      <td>female</td>
      <td>Marvel</td>
      <td>1939.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Batman</td>
      <td>good</td>
      <td>male</td>
      <td>DC</td>
      <td>1934.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Joker</td>
      <td>bad</td>
      <td>male</td>
      <td>DC</td>
      <td>1934.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Catwoman</td>
      <td>bad</td>
      <td>female</td>
      <td>DC</td>
      <td>1934.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Hellboy</td>
      <td>good</td>
      <td>male</td>
      <td>Dark Horse Comics</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Image</td>
      <td>1992.0</td>
    </tr>
  </tbody>
</table>
</div>



**Left Join**

{{< figure src="./left_join.png" >}}


```python
pd.merge(df1, df2, how = "left", on = "publisher")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>alignment</th>
      <th>gender</th>
      <th>publisher</th>
      <th>year_founded</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Magneto</td>
      <td>bad</td>
      <td>male</td>
      <td>Marvel</td>
      <td>1939.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Storm</td>
      <td>good</td>
      <td>female</td>
      <td>Marvel</td>
      <td>1939.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mystique</td>
      <td>bad</td>
      <td>female</td>
      <td>Marvel</td>
      <td>1939.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Batman</td>
      <td>good</td>
      <td>male</td>
      <td>DC</td>
      <td>1934.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Joker</td>
      <td>bad</td>
      <td>male</td>
      <td>DC</td>
      <td>1934.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Catwoman</td>
      <td>bad</td>
      <td>female</td>
      <td>DC</td>
      <td>1934.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Hellboy</td>
      <td>good</td>
      <td>male</td>
      <td>Dark Horse Comics</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## 7. Apply and groupby

### 7.1. Apply

Trong Python, có hai loại hàm: Một là các hàm nhận đối số đầu vào là một mảng và trả về một mảng. Một loại khác thì ngược lại, chỉ nhận đối số đầu vào là một scalar. Do đó cũng có hai phương thức được xây dựng tương ứng với hai loại hàm này, để áp dụng một hàm với từng phần tử trong DataFrame.

- `df.apply()`: Sử dụng với loại hàm thứ nhất.
- `df.applymap()`: Sử dụng với loại hàm thứ hai.


```python
df = pd.read_csv('./cycling_data.csv')
df[['Time', 'Distance']].apply(np.sin)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Time</th>
      <th>Distance</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.901866</td>
      <td>0.053604</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.901697</td>
      <td>0.447197</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.035549</td>
      <td>-0.046354</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.739059</td>
      <td>0.270228</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.236515</td>
      <td>-0.086263</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>-0.683372</td>
      <td>0.063586</td>
    </tr>
    <tr>
      <th>29</th>
      <td>0.150056</td>
      <td>0.133232</td>
    </tr>
    <tr>
      <th>30</th>
      <td>0.026702</td>
      <td>0.023627</td>
    </tr>
    <tr>
      <th>31</th>
      <td>-0.008640</td>
      <td>0.221770</td>
    </tr>
    <tr>
      <th>32</th>
      <td>0.897861</td>
      <td>-0.700695</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 2 columns</p>
</div>




```python
df[['Time']].apply(lambda x: x / 3600)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.578889</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.703056</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.517500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.608889</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.525278</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>0.519444</td>
    </tr>
    <tr>
      <th>29</th>
      <td>0.596944</td>
    </tr>
    <tr>
      <th>30</th>
      <td>0.511389</td>
    </tr>
    <tr>
      <th>31</th>
      <td>0.684167</td>
    </tr>
    <tr>
      <th>32</th>
      <td>0.511944</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 1 columns</p>
</div>




```python
int([5, 10])
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_5224/327221190.py in <module>
    ----> 1 int([5, 10])
    

    TypeError: int() argument must be a string, a bytes-like object or a real number, not 'list'



```python
df[['Time']].applymap(int)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2084</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2531</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1863</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2192</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1891</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1870</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2149</td>
    </tr>
    <tr>
      <th>30</th>
      <td>1841</td>
    </tr>
    <tr>
      <th>31</th>
      <td>2463</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1843</td>
    </tr>
  </tbody>
</table>
<p>33 rows × 1 columns</p>
</div>



### 7.2. Groupby

Hàm `df.groupby()` được sử dụng để nhóm dữ liệu thành các nhóm, sau đó ta có thể sử dụng các hàm thống kê cho từng nhóm này.

{{< figure src="./groupby_2.png" >}}


```python
dfg = df.groupby(by = 'Name')
dfg.groups
```




    {'Afternoon Ride': [0, 2, 4, 6, 9, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32], 'Morning Ride': [1, 3, 5, 7, 8, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31]}




```python
dfg.mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Time</th>
      <th>Distance</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Afternoon Ride</th>
      <td>4654.352941</td>
      <td>12.462</td>
    </tr>
    <tr>
      <th>Morning Ride</th>
      <td>2299.875000</td>
      <td>12.860</td>
    </tr>
  </tbody>
</table>
</div>




```python
dfg.aggregate(['mean', 'sum', 'count'])
```

    C:\Users\ktuyends\AppData\Local\Temp/ipykernel_5224/914058847.py:1: FutureWarning: ['Date', 'Type', 'Comments'] did not aggregate successfully. If any error is raised this will raise in a future version of pandas. Drop these columns/ops to avoid this warning.
      dfg.aggregate(['mean', 'sum', 'count'])
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">Time</th>
      <th colspan="3" halign="left">Distance</th>
    </tr>
    <tr>
      <th></th>
      <th>mean</th>
      <th>sum</th>
      <th>count</th>
      <th>mean</th>
      <th>sum</th>
      <th>count</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Afternoon Ride</th>
      <td>4654.352941</td>
      <td>79124</td>
      <td>17</td>
      <td>12.462</td>
      <td>186.93</td>
      <td>15</td>
    </tr>
    <tr>
      <th>Morning Ride</th>
      <td>2299.875000</td>
      <td>36798</td>
      <td>16</td>
      <td>12.860</td>
      <td>205.76</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>



## 8. Summary

Như vậy, trong bài viết này chúng ta đã đi qua hầu hết những thứ cơ bản trong Pandas.

**Làm quen với Pandas**

- Tạo Series với `pd.Series()` 
- Tạo DataFrames với `pd.DataFrame(array_2d, index, column)`
- Indexing và slicing với: `df[], df.loc[], df.iloc[], df.query()`
- Các toán tử giữa 2 Series kết hợp với nhau dựa vào labels.
- Import data với `pd.read_csv`

**Basic data wrangling**

- Xem thông tin về DataFrame với `df.head()`, `df.tail()`, `df.info()`, `df.describe()`
- Đổi tên cột với `df.columns` và `df.rename()`
- Thay đổi index với `df.set_index()`, `df.index.name`, `df.reset_index()`, `df.index`
- Thêm cột với `df['variable_name']`
- Thêm hàng với `df.append()`
- Xóa cột hoặc hàng với `df.drop(columns)` và `df.drop(index)`
- DataFrame reshaping với `df.melt()`, `df.pivot()`, `df.pivot_table()`
- Gộp hai bảng dữ liệu với `df.concat()`, `df.merge()`
- Áp dụng một hàm với từng phần tử sử dụng `df.apply()` và `df.applymap()`
- Groupby và Aggregate với `df.groupby()`
