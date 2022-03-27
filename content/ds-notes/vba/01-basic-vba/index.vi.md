---
title: "VBA for Creative Problem Solving, Part 1"
subtitle: ""
slug: basic-vba
date: 2022-03-26
lastmod: 2022-03-26
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Excel VBA"]
categories: []
series: [VBA Programming]
series_weight: 1
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->

## 1. Làm quen với VBA

### 1.1. Bắt đầu

Đầu tiên, ta cần phải bật tab _Developer_ bằng cách vào `File -> Options -> Customize Ribbon -> Developer` và ta có kết quả như sau:

{{< figure src="developer.png" >}}

Như chúng ta có thể thấy ở phần Code của tab Developer:

- Visual Basic: Để vào cửa sổ soạn thảo VBA.
- Record Macro: Để bắt đầu tạo các macro.

Để bắt đầu viết code VBA, ta chọn _Visual Basic_ sau đó vào _Insert -> Module_. Một chương trình đơn giản:

```vbnet
' Đây là một comment
Sub Test()
MsgBox "Today is a newday"
End Sub
```

### 1.2. Tạo macros

Để tạo Macro, chúng ta vào `Developer -> Record Macro`, sau đó đặt phím tắt và tên cho macro, cuối cùng click vào `OK` để bắt đầu ghi macro.

Bây giờ, ta có thể thực hiện các thao tác với Cell, Worksheet,...cho đến khi hoàn thành thì ta chọn _Stop Recording_.

Để xem chương trình được tạo ra cho Macro, ta vào `Developer -> Visual Basic`.

### 1.3. Tham chiếu tương đối và tuyệt đối

- Khi sử dụng tham chiếu tuyệt đối, Excel sẽ áp dụng Macro đối với các Cells cố định khi thực thi.
- Khi sử dụng tham chiếu tương đối (Relative), Excel áp dụng Macro dựa vào vị trí của con trỏ chuột.

### 1.3. Subroutines và Functions

- Function sẽ nhận các đầu vào, thực hiện các tính toán và trả về kết quả được tính toán khi gọi hàm.
- Sub không trả về một kết quả, nó chỉ thực hiện các hoạt động được ghi lại khi chúng ta gọi macros.

### 1.4. Option Explicit

Với nhiều ngôn ngữ, khi lập trình chúng ta phải khai báo biến trước khi sử dụng. Nhưng trong VBA, chúng ta có thể không cần khai báo biến để sử dụng. Tuy nhiên, khi có thêm lựa chọn _Option Explicit_ thì nó yêu cầu ta phải khai báo biến mới được phép sử dụng.

```vbnet
Option Explicit
' ... code VBA phía dưới
```

### 1.5. Khai báo biến

Cú pháp:

```vbnet
' Phạm vi hoạt động: Dim, Public, Private, Static,
' data_type là kiểu dữ liệu của biến
[Phạm vi hoạt động] my_var as data_type
```

**Biến toàn cục và biến cục bộ**

- Biến toàn cục là biến được dùng chung ở nhiều Sub/Function khác nhau mà chỉ cần khai báo một lần.
- Biến cục bộ (local) là biến chỉ dùng được trong một Sub/Function và khi kết thúc Sub/Function thì biến này cũng bị giải phóng.

**Các từ khóa khai báo phạm vi biến**

- Public: Biến toàn cục có thể dùng ở bất cứ đâu trong Workbook, khai báo ở đầu module, bên ngoài Sub/Function.
- Private: Là biến toàn cục nơi được khai báo, nhưng chỉ được phép hoạt động ở trong môi trường đó. Ví dụ, khi khai báo bên trong Sub hoặc Function thì nó là biến cục bộ của Sub hoặc Function đó, còn khai báo ở đầu Module thì nó là biến cục bộ của Module đó.
- Dim: Dùng để khai báo các biến cục bộ trong các Sub, Function
- Static: Là biến cục bộ trong Sub, Function nhưng giá trị của nó được lưu lại cho đến khi thoát file.

**Một số kiểu dữ liệu trong VBA**

| Kiểu dữ liệu |                    Ý Nghĩa                    |
| :----------: | :-------------------------------------------: |
|    Double    |                    Số thực                    |
|   Integer    |                   Số nguyên                   |
|    String    |                Chuỗi các ký tự                |
|   Boolean    |               Kiểu True, False                |
|   Objects    | Một số kiểu đặc biệt như Range, Worksheet,... |

## 2. Định nghĩa Functions

### 2.1. Các toán tử

- Toán tử cơ bản: _+, -, \*, /, ^ (lũy thừa), \ (integer division), mod_
- Toán tử nối: _'strA' & 'strB'_
- Toán tử so sánh: _>, >=, <, <=, =, <> (không bằng)_
- Toán tử logic: _Not, And, Or_

{{< admonition type=notes title="Lưu ý" open=true >}}
VBA không phân biệt giữa ký tự in hoa và in thường
{{< /admonition >}}

### 2.2. Một số hàm được xây dựng sẵn

|     |                |       |       |          |
| --- | -------------- | ----- | ----- | -------- |
| Abs | Sin            | Int   | Val   | MsgBox   |
| Sqr | Cos            | Len   | Str   | InputBox |
| Exp | Tan            | Left  | UCase | Time     |
| Log | 4\*Atn(1) = pi | Right | LCase | Date     |
| Rnd | Timer          | Mid   | InStr | Array    |

### 2.3. Sử dụng các hàm Excel trong VBA

Để sử dụng các hàm của Excel trong VBA, chúng ta sử dụng cú pháp: `Application.WorksheetFunction.func_name()`

### 2.4. Định nghĩa hàm

```vbnet
' Khởi tạo hàm
Function my_func(inputA As Double, inputB As String) As Double

' Khai báo biến
Dim my_var As Double

' Thực hiện các tính toán
' Trả về kết quả
my_func = value

End Function
```

### 2.5. Lập trình Modular

```vbnet
' Sub1
Sub SomeSub1()
...
End Sub

' Sub2
Sub SomeSub2()
...
End Sub

' Function(X)
Function SomeFunction(X)
...
End Function
```

```vbnet
' Modular Programming
Sub ThisSub()
...
Call SomeSub1
...
Call SomeSub2
...
z = SomeFunction(X)
...
End Sub
```

## 3. Tương tác giữa Excel và VBA

### 3.1. Các đối tượng trong VBA

{{< figure src="objects.png" >}}

Tập hợp các đối tượng:

- Workbooks: Tất cả các workbooks đang mở
- Worksheets: Tất cả các sheet trong workbook
- Charts: Tất cả các chart trong workbook

Cú pháp tham chiếu đến một đối tượng:

```vbnet
' Một số cách
Application.Workbooks("file_name").Worksheets("Sheet_name").Range("B52")
Workbooks("file_name").Worksheets("Sheet_name").Range("B52")
Worksheets("Sheet_name").Range("B52")
Range("B52")
```

### 3.2. Phương thức, thuộc tính

- Thuộc tính: Các đặc điểm của một đối tượng, ví dụ `Range("B1").Width` mô tả độ rộng của một ô `B1`.
- Phương thức: Các hàm, hành động tác động đến một đối tượng, ví dụ `Range("B1").Clear` thực hiện hành động xóa nội dung trong ô `B1`.
- Events (sự kiện): Mô tả phản ứng của một đối tượng đối với một hành động, ví dụ như khi ta click chuột hoặc mở một workbook,...

**Một số phương thức, thuộc tính**

|                       |                    |
| --------------------- | ------------------ |
| Range (object)        | Rows (Property)    |
| Select (Method)       | Columns (Property) |
| Selection (Property)  | Count (Property)   |
| Activate (Method)     | Cells (Property)   |
| ActiveCell (Property) | Offset (Property)  |

### 3.3. Làm việc với Range

**Lựa chọn**

```vbnet
' Tham chiếu
Range("D22")
Range("A1:B5")
Range("customer")

' Tham chiếu đến các cột
Range("D:D")
Range("D:F")

' Tham chiếu đến các hàng
Range("3:3")
Range("3:10")
```

```vbnet
' Tham chiếu đến ô
Cells(row_idx, col_idx)

' Offset
Range("B1").Offset(1, 2)
```

```vbnet
' Selection
Range("A2:C6").Select
Selection 'Chính là Range("A1:A10")

Range("A2:C6").Range("B2")
Selection.Range("B2")
```

{{< admonition type=notes title="Select và Activate" open=true >}}

- Select là việc lựa chọn một hoặc nhiều cell, worksheet,...
- Activate là kích hoạt một cell, worksheet,...
- Chúng ta có thể lựa chọn nhiều cell, worksheet...nhưng trong những đối tượng đó chỉ có một cell hoặc worksheet được kích hoạt.
  {{< /admonition >}}

**Phương thức count**

```vbnet
' Đếm số ô
Range("A1:C3").Count

' Đếm số hàng, cột
Range("A1:C3").Rows.Count
Range("A1:C3").Columns.Count
```

## 4. Cấu trúc lập trình VBA

### 4.1. Câu lệnh IF

```vbnet
' Câu lệnh đơn giản
If <dieu_kien> Then
    ' Do Something
End If

' Mở rộng câu lệnh If
If <dieu_kien> Then
    ' Do Something
Else
    ' Do Something
End If
```

```vbnet
' Câu lệnh If tổng quát
If <dieu_kien> Then
' code block 1
ElseIf <dieu_kien> Then
' code block 2
...
Else
' code block n
End If
```

### 4.2. Vòng lặp For Next

```vbnet
' Lặp với số lần xác định
For i = 1 To n
' Do something
Next i

' For step
For i = 1 To n Step 2
' Do something
Next i
```

```vbnet
' Thoát khỏi vòng lặp
Exit For

' Bỏ qua lần lặp hiện tại và nhảy tới lần lặp kế tiếp
Continue For
```

### 4.3. Vòng lặp For Each

Vòng lặp này, lặp qua từng phần tử của một danh sách (Collection) ví dụ như lặp qua các ô, các sheet trong Excel. Cú pháp:

```vbnet
For Each <Object> In Collection
    ' Do Something
Next <Object>
```

### 4.4. Vòng lặp Do While

```vbnet
' Lặp với số lần không xác định
' Kiểm tra điều kiện ở đầu vòng lặp
Do While <condition>
   ' Do something
   Exit Do
Loop

' Kiểm tra điều kiện ở cuối vòng lặp
Do
   ' Do something
   Exit Do
Loop While <condition>
```

### 4.5. Vòng lặp Do Until

Ngược lại với vòng lặp `Do - While`

### 4.6. Mệnh đề Select Case

```vbnet
Select Case expression
   Case expressionlist1
      statement1
      statement2
      ....
   Case expressionlist2
      statement1
      statement2
      ....
   Case expressionlistn
      statement1
      statement2
      ....
   Case Else
      elsestatement1
      elsestatement2
      ....
End Select
```
