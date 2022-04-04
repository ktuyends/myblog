---
title: Truy vấn SQL Server trong Jupyter Notebooks
slug: jupyter-notebooks-for-sql-server
subtitle: ""
summary: Khi sử dụng Python, có đôi lúc chúng ta sẽ cần lấy dữ liệu từ Database vào Python. Trong bài viết này, mình sử dụng thư viện `pyodbc` và `ipython-sql` để kết nối và tương tác với SQL Server.
date: "2021-10-09"
lastmod: "2021-10-09"
draft: false
authors: ["Tuyen Kieu"]
images: ["featured.png"]
tags: ["Blog"]
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

Khi sử dụng Python, có đôi lúc chúng ta sẽ cần lấy dữ liệu từ Database vào Python. Trong bài viết này, mình sử dụng thư viện `pyodbc` để kết nối với database, `ipython-sql` để tương tác với SQL Server trong Jupyter.

## 1. Cài đặt và kết nối

### 1.1. Cài đặt và import thư viện `pyodbc`

Để kết nối Python với SQL Server chúng ta sử dụng thư viện `pyodbc`. Trước tiên ta cần cài đặt `pyodbc` sử dụng pip hoặc conda:

```python
# Cài đặt bằng pip
pip install pyodbc

# Cài đặt bằng conda
conda install pyodbc
```

Sau khi cài đặt `pyodbc`, ta import thư viện vào Python và kiểm tra xem có những giao thức nào hiện có để kết nối với database:

```python
import pyodbc
pyodbc.drivers()
```

```
['SQL Server',
 'PostgreSQL ANSI(x64)',
 'PostgreSQL Unicode(x64)',
 'Amazon Redshift (x64)',
 'SQL Server Native Client 11.0',
 'SQL Server Native Client RDA 11.0',
 'Microsoft Access Driver (*.mdb, *.accdb)',
 'Microsoft Excel Driver (*.xls, *.xlsx, *.xlsm, *.xlsb)',
 'Microsoft Access Text Driver (*.txt, *.csv)',
 'ODBC Driver 17 for SQL Server']
```

Ồ có khá nhiều drivers, cơ mà mình cũng không hiểu rõ lắm về những drivers này. Trong bài viết này, mình sẽ sử dụng `ODBC Driver 17 for SQL Server`.

### 1.2. Kết nối với database

Về cơ bản, ta có cú pháp sau:

```python
conx = pyodbc.connect('DRIVER={SQL Server};'
                      'SERVER=TestServer;'
                      'Database=TestDatabase;'
                      'UID=UserID; PWD=Password;')
```

Nếu các bạn sử dụng Windows Authentication, thì chúng ta cần sửa đổi lại cú pháp một chút:

```python
conx = pyodbc.connect('DRIVER={SQL Server};'
                      'SERVER=TestServer;'
                      'Database=TestDatabase;'
                      'TRUSTED_CONNECTION=yes')
```

Để lấy thông tin về Server, database các bạn sử dụng SQL Server Management Studio:

<p align="center"><img src="sql.png"></p>

<p align="center"><img src="sql2.png"></p>

Hoặc thực hiện truy vấn trong SQL:

```sql
SELECT @@SERVERNAME
```

Cuối cùng ta có kết quả như sau:

```python
conn1 = pyodbc.connect("DRIVER={ODBC Driver 17 for SQL Server};"
                       "SERVER=KTUYEN-PC\DSSQL2019;"
                       "Database=AdventureWorks2019;"
                       "TRUSTED_CONNECTION=yes;")
```

### 1.3. Thực hiện truy vấn sử dụng `pyodbc`

Quy trình:

```python
# Create a CONNECTION using the connection string and pyodbc.connect()
conx = pyodbc.connect(conx_string)

# Create a CURSOR that we can use to work in the database
cursor = conx.cursor()

# Run the QUERY using cursor.execute()
cursor.execute(query)

# Store the RESULTS in a variable
data = cursor.fetchall()

# Display the RESULTS to check the data
print(data)

# Close the CONNECTION using the methodclose()
conx.close()
```

Ví dụ:

```python
# Khởi tạo con trỏ
cursor = conn1.cursor()

# Query
query = """
SELECT TOP 10 Name, CreditRating
FROM Purchasing.Vendor
WHERE CreditRating < 3
"""

# Execute
cursor.execute(query)

# Store
data = cursor.fetchall()

# print
print(data)
```

```
[('Australia Bike Retailer', 1), ('Allenson Cycles', 2), ('Advanced Bicycles', 1), ('Trikes, Inc.', 2), ('Morgan Bike Accessories', 1), ('Cycling Master', 1), ('Chicago Rent-All', 2), ('Greenwood Athletic Company', 1), ('Compete Enterprises, Inc', 1), ('International', 1)]
```

### 1.4. Thực hiện truy vấn sử dụng `pandas`

Như các bạn thấy, kết quả hiển thị như trên có vẻ không thuận tiện lắm cho việc xử lý dữ liệu. Vì vậy, chúng ta nên chuyển đổi nó thành DataFrame bằng cách sử dụng thư viện `pandas`:

```python
# import pandas
import pandas as pd

# Getting data using pd.read_sql(query, connection)
data = pd.read_sql(query, conn1)

# Xem kết quả
data
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
      <th>CreditRating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Australia Bike Retailer</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Allenson Cycles</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Advanced Bicycles</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Trikes, Inc.</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Morgan Bike Accessories</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Cycling Master</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chicago Rent-All</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Greenwood Athletic Company</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Compete Enterprises, Inc</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>International</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>

## 2. Jupyter Magics

Jupyter Notebooks có thể tương tác với SQL thông qua công cụ Jupyter Magics, nhưng ta phải cài đặt thư viện `ipython-sql`:

```python
# cài đặt ipython-sql
conda install ipython-sql
```

Sau khi cài đặt, ta chạy câu lệnh dưới để bắt đầu:

```python
%load_ext sql
```

### 2.1. Kết nối với database

Tương tự như phần trước, đầu tiên chúng ta cần phải kết nối Python/Jupyter với database sử dụng cú pháp sau:

```python
mssql+pyodbc://user:password@server:port/DatabaseName?driver=DriverName
```

Nếu các bạn sử dụng Windows Authentication thì:

```python
mssql+pyodbc://user@server:port/DatabaseName?trusted_connection=yes&driver=DriverName
```

Kết quả:

```python
%sql mssql+pyodbc://ktuyends@KTUYEN-PC\DSSQL2019/AdventureWorks2019?trusted_connection=yes&driver=ODBC+Driver+17+for+SQL+Server
```

```
'Connected: ktuyends@AdventureWorks2019'
```

### 2.2. Thực hiện truy vấn

Ta có một số trường hợp như sau:

- Sử dụng `%sql` nếu các câu lệnh truy vấn nằm trên cùng 1 dòng
- Sử dụng `%%sql` nếu các câu lệnh truy vấn nằm trên nhiều dòng
- Sử dụng `%sql $query_var` với `query_var` là biến string gồm nhiều câu lệnh truy vấn

Ví dụ:

```python
%sql SELECT TOP 5 Name, CreditRating FROM Purchasing.Vendor
```

```
 * mssql+pyodbc://ktuyends@KTUYEN-PC\DSSQL2019/AdventureWorks2019?driver=ODBC+Driver+17+for+SQL+Server&trusted_connection=yes
 Done.
```

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>CreditRating</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Australia Bike Retailer</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Allenson Cycles</td>
            <td>2</td>
        </tr>
        <tr>
            <td>Advanced Bicycles</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Trikes, Inc.</td>
            <td>2</td>
        </tr>
        <tr>
            <td>Morgan Bike Accessories</td>
            <td>1</td>
        </tr>
    </tbody>
</table>

```sql
%%sql

SELECT TOP 7 Name, CreditRating
FROM Purchasing.Vendor
WHERE CreditRating < 10
```

```
 * mssql+pyodbc://ktuyends@KTUYEN-PC\DSSQL2019/AdventureWorks2019?driver=ODBC+Driver+17+for+SQL+Server&trusted_connection=yes
Done.
```

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>CreditRating</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Australia Bike Retailer</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Allenson Cycles</td>
            <td>2</td>
        </tr>
        <tr>
            <td>Advanced Bicycles</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Trikes, Inc.</td>
            <td>2</td>
        </tr>
        <tr>
            <td>Morgan Bike Accessories</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Cycling Master</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Chicago Rent-All</td>
            <td>2</td>
        </tr>
    </tbody>
</table>

```python
# tạo biến query_var
query_var = """
SELECT TOP 5 Name, CreditRating
FROM Purchasing.Vendor
WHERE CreditRating < 10
"""

# thực hiện truy vấn và gán kết quả
data = %sql $query_var
data
```

```
 * mssql+pyodbc://ktuyends@KTUYEN-PC\DSSQL2019/AdventureWorks2019?driver=ODBC+Driver+17+for+SQL+Server&trusted_connection=yes
Done.
```

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>CreditRating</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Australia Bike Retailer</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Allenson Cycles</td>
            <td>2</td>
        </tr>
        <tr>
            <td>Advanced Bicycles</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Trikes, Inc.</td>
            <td>2</td>
        </tr>
        <tr>
            <td>Morgan Bike Accessories</td>
            <td>1</td>
        </tr>
    </tbody>
</table>

Bài này đến đây là kết thúc, dù sao mục đích ban đầu của mình cũng chỉ là thử nghiệm. Còn khá nhiều vấn đề cần khám phá, có lẽ sau này mình sẽ đi sâu hơn.
