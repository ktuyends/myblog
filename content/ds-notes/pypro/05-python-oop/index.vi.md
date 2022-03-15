---
title: "Pypro - Lập trình hướng đối tượng"
subtitle: ""
slug: python-oop
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
## 1. Biến trong Python

Trong Python, mọi thứ đều là đối tượng, và một biến chỉ đơn giản là một tên, mang ý nghĩa tượng trưng, trỏ đến một đối tượng trong bộ nhớ. 

Ví dụ:

```python
# Phép gán
my_var = 100

# xem địa chỉ trong bộ nhớ của my_var
id(my_var)

# Xem kiểu dữ liệu của biến
type(my_var)
```

**Phép gán:**

```python
# Gán một giá trị cho một biến
my_var = 10

# Gán một giá trị cho nhiều biến
a = b = c = 10

# Gán nhiều giá trị cho nhiều biến
a, b = (5, 10)
a, b = 5, 10

# Lưu ý với string
a, b, c, d, e, f = 'Python'
a # 'P'

# đổi giá trị giữa 2 biến
x = 5
y = 10
x, y = y, x
```

{{< admonition type=notes title="Một số lưu ý về tên biến" open=true >}}
- Tên biến trong Python chỉ bao gồm các chữ cái, số và dấu gạch dưới `_`
- Tên biến phân biệt giữa các ký tự in hoa và in thường
- Tên biến không được trùng với các từ khóa trong Python
- Tên biến không được bắt đầu bằng số
{{< /admonition >}}

## 1. Syntax

- Tạo hàm
- if, elif, else
- assert
- for, while
- Comprehension


## 2. Numbers

- Các toán tử khi làm việc vơi số
- Các vấn đề với float, decimal, fraction
- So sánh == với kiểu float: math.isclose()
- Chuyển đổi giữa 3 loại 
- Làm tròn


