---
title: "Làm quen với lập trình VBA"
subtitle: ""
slug: intro-to-vba-programming
summary: "VBA là viết tắt của Visual Basic Application, ta có thể hiểu nó như là một ứng dụng lập trình cơ bản trong Microsoft Office."
date: 2022-03-30
lastmod: 2022-03-30
draft: false
authors: ["Tuyen Kieu"]
images: ["featured.png"]
tags: ["Blog", "VBA Programming"]
toc:
  enable: true
license: ""
hiddenFromHomePage: false
lightgallery: true
---

VBA là viết tắt của Visual Basic Application, ta có thể hiểu nó như là một ứng dụng lập trình cơ bản trong _Microsoft Office_. VBA thường được sử dụng trong việc tự động hóa các tác vụ Excel hoặc xây dựng các hàm mở rộng khi Excel không có.

Về bài viết này, thì đây không phải là một bài viết về lập trình VBA. Bài viết này chỉ mang tính vọc vạch, tò mò của mình về VBA nên mình mới nghịch chơi chơi thôi.

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

### 1.4. Subroutines và Functions

- Function sẽ nhận các đầu vào, thực hiện các tính toán và trả về kết quả được tính toán khi gọi hàm.
- Sub không trả về một kết quả, nó chỉ thực hiện các hoạt động được ghi lại khi chúng ta gọi macros.

### 1.5. Option Explicit

Với nhiều ngôn ngữ, khi lập trình chúng ta phải khai báo biến trước khi sử dụng. Nhưng trong VBA, chúng ta có thể không cần khai báo biến để sử dụng. Tuy nhiên, khi có thêm lựa chọn _Option Explicit_ thì nó yêu cầu ta phải khai báo biến mới được phép sử dụng.

```vbnet
Option Explicit
' ... code VBA phía dưới
```

### 1.6. Khai báo biến

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
|   Variant    |          Kiểu dữ liệu không xác định          |

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

## 5. Làm việc với mảng

### 5.1. Mảng trong Excel

**Ví dụ 1:** Lặp qua các ô trong mảng, sau đó với mỗi ô đó ta cộng thêm giá trị 5.

```vbnet
Sub AddFive()

' Khai báo biến
Dim i As integer
Dim j As integer
Dim nr As integer
Dim nc As integer

' Đếm số hàng, cột
nr = Selection.Rows.Count
nc = Selection.Columns.Count

' Vòng lặp
For i = 1 to nr
  For j = 1 to nc
    Selection.Cells(i, j) = Selection.Cells(i, j) + 5
  Next j
Next i

End Sub
```

**Ví dụ 2:** Tạo một mảng mới, có kích thước giống với mảng ban đầu, và giá trị trong mỗi ô bằng giá trị trong ô tương ứng của mảng ban đầu công thêm 5.

```vbnet
Sub AddFive()

' Khai báo biến
Dim i As integer
Dim j As integer
Dim nr As integer
Dim nc As integer

' Đếm số hàng, cột
nr = Selection.Rows.Count
nc = Selection.Columns.Count

' Vòng lặp
For i = 1 to nr
  For j = 1 to nc
    ActiveCell.Offset(nr + i, j - 1) = Selection.Cells(i, j) + 5
  Next j
Next i

End Sub
```

### 5.2. Mảng trong VBA

**Ví dụ 3:** Tạo một mảng có kích thước _2x2_

```vbnet
' Chỉ số của mảng bắt đầu từ 1, mặc định là 0
Option Base 1

' Tạo mảng
Sub CreateArray()

' Khai báo và tạo mảng
Dim A(2, 2) As Integer
A(1, 1) = 3
A(1, 2) = 4
A(2, 1) = 5
A(2, 2) = 6

' Export to Excel
Range("A1:B2") = A

End Sub

' Kích thước mạng
LBound()
UBound()
```

### 5.3. Di chuyển giữa mảng Excel và VBA

**Ví dụ 4:** Import dữ liệu từ Excel

```vbnet
' Cách 1:
Sub ImportArray()

' Khai báo biến
Dim i As integer
Dim j As integer
Dim nr As integer
Dim nc As integer
Dim A() As integer

' Đếm số hàng, cột
nr = Selection.Rows.Count
nc = Selection.Columns.Count

' Đổi kích thước ReDim
ReDim A(nr, nc) As integer

' Import
For i = 1 to nr
  For j = 1 to nc
    A(i, j) = Selection.Cells(i, j)
  Next j
Next i

End Sub
```

```vbnet
' Cách 2
Sub ImportArray()

' Khai báo mảng động
Dim A() As Variant

A = Range("A1:C3")
End Sub
```

**Ví dụ 5:** Export dữ liệu từ VBA đến Excel

```vbnet
Sub ExportArray()

' Khai báo
Dim i As integer
Dim j As integer
Dim A(3, 3) As integer

' Export to Excel
For i = 1 to 3
  For j = 1 to 3
    A(i, j) = 2 * i + j
    Range("B2:D4).Cells(i, j) = A(i, j)
  Next j
Next i

' Sử dụng Selection
Selection = A

End Sub
```

### 5.4. Định nghĩa hàm mảng

Hàm mảng, là hàm nhận đối số đầu vào là một mảng.

```vbnet
' Hàm trả về một số
Function my_func(rng As Range, n As integer) As integer
' Do Something

' Return
my_func = value
End Function
```

```vbnet
' Hàm trả về một mảng
Function my_func(rng As Range, n As integer) As Variant

' Khai báo mảng
Dim B() As Variant

' Return
my_func = B
End Function
```

### 5.5. ReDim Preserve

Theo mặc định, khi sử dụng `ReDim` để thay đổi kích thước mảng, nó sẽ xóa toàn bộ các giá trị được lưu trữ trong mảng. Trong trường hợp, ta muốn giữ lại các giá trị này ta phải sử dụng: `ReDim Preserver Array(m, n)`

## 6. Làm việc với string

Một số hàm hay sử dụng:

| Excel              | VBA                |
| ------------------ | ------------------ |
| LEFT/MID/RIGHT     | Left, Mid, Right   |
| LEN                | Len                |
| FIND/SEARCH        | InStr(str, substr) |
| UPPER/LOWER/PROPER | UCase, LCase       |
| TEXTJOIN           | JOIN (on a array)  |
| CONCATENATE        | A & B              |
|                    | Split              |

## 7. Làm việc với worksheets và workbooks

### 7.1. Worksheets

Một số phương thức, thuộc tính của Worksheets:

```vbnet
' Đếm Sheets
Worksheets.Count

' Tên
Worksheets(i).Name
ActiveSheet.Name

' Đổi tên
Sheets("Sheet3").Name = "New Name"
```

```vbnet
' Thêm Sheets
Sheets.Add After:=ActiveSheet

' Xóa
Sheets("Sheet2").Delete

' Ẩn
Sheets("Sheet2").Visible = False

' Active
Sheets("Sheet2").Active
Worksheets("Sheet2").Active
Sheets(2).Active

'Tắt cảnh báo
Application.DisplayAlerts = False
```

### 7.2. Vòng lặp với worksheets

```vbnet
' Ví dụ 1
Sub NewExampl()
Dim w As Worksheets

For Each w in Worksheets
  w.Range("B2") = 10
Next
End Sub

' Ví dụ 2
Sub IterWorksheets()
Dim i As Integer
Dim n As Integer

n = Worksheets.Count

For i = 1 to n
  Worksheets(i).Range("B2") = 10
Next i

End Sub
```

### 7.3. Workbooks

Một số phương thức và thuộc tính:

```vbnet
' Đếm
Workbooks.Count

' Tên
Workbooks(i).Name
ActiveWorkbooks.Name

' Close workbooks
Workbooks(2).Close SaveChanges:=True

' Thêm
Workbooks.Add

' Save
ActiveWorkbooks.SaveAs Filename:="path", FileFormat:=, CreateBackup:=False

' Active
Workbooks("file").Active
Set tWb = ThisWorkbook
Set aWb = ActiveWorkbook

' Đóng
wb.Close
```

{{< admonition type=notes title="ThisWorbook và ActiveWorkbook" open=true >}}

- ThisWorkbook là nơi tạo Macro
- ActiveWorkbook là workbook đang hoạt động
  {{< /admonition >}}

### 7.4. Mở workbooks

```vbnet
' Mở một file
Workbooks.Open file_name

' Mở một file bằng thao tác
FileName = Application.GetOpenFilename(FileFilter:="Excel Filter (*.xlsx), *.xlsx, Title:= Open File(s)", MultiSelect:=False)
Workbooks.Open FileName
```

## 8. Lập trình user forms

### 8.1. Input boxes

Cú pháp:

`InputBox(prompt, [Title], [Default], [Xpos], [YPos], [HelpFile], [Context], [Type])`

Trong đó:

- Prompt: Nội dung thông báo
- Title: Tiêu đề của hộp thoại
- Default: Giá trị mặc định
- Type: Kiểu dữ liệu được phép nhập

Ví dụ:

```vbnet
Sub Test()
Dim x As Variant
Do
    x = Application.InputBox(Prompt:="Please enter something", Title:="Input", Default:=7, Type:=2)
    If x <> False Then
      Exit Do
    MsgBox "You didn't enter anything! Try again."
Loop
End Sub
```

### 8.2. MsgBox

Cú pháp:

`MsgBox("Prompt",[Buttons],[Title],[Helpfile],[Context])`

Một số giá trị mà khi chúng ta click vào buttons sẽ trả về:

- vbOK: 1
- vbCancel: 2
- vbAbort: 3
- vbRetry: 4
- vbIgnore: 5
- vbYes: 6
- vbNo: 7

### 8.3. User forms

Để bắt đầu tạo user forms, ta vào _Insert -> UserForm_, sau đó ta sẽ có một giao diện như này:

{{< figure src="userform.png" width=80% >}}

Tiếp theo chúng ta sẽ kéo các công cụ bên trong Toolbox vào phần UserForm để thiết kế giao diện người dùng. Với mỗi Control chúng ta có một bảng thuộc tính Properties tương ứng.

Ví dụ một user form đơn giản sử dụng Label, Text Box, Frame, OptionButton và CommandBotton

{{< figure src="userform-examp.png" width=60% >}}

Mặc dù giao diện đã hình thành, nhưng nó lại không thể thực hiện các hoạt động. Vì vậy ta cần phải lập trình cho các controls. Ta click vào các controls để vào phần lập trình tương ứng với control đó.

```vbnet
Option Explicit

Private Sub CalculateButton_Click()
If Multiply Then
    Output = Ainput * Binput
Else
    Output = Ainput / Binput
End If
End Sub

Private Sub QuitButton_Click()
UserForm1.Hide
End Sub

Private Sub ResetButton_Click()
Unload UserForm1
UserForm1.Show
End Sub
```

## 9. Case study

### 9.1. Giới thiệu về Case study

Trong Case study này, chúng ta sẽ đi xây dựng một User Form cho phép người dùng sử dụng tỷ giá hối đoái thực tế ở một thời điểm xác định để chuyển đổi tiền tệ từ đơn vị này sang đơn vị khác. Ngoài ra, nó còn cho phép người dùng xem biểu đồ tỷ giá hối đoái trong vòng 30 ngày gần nhất với ngày được xác định.

Quy trình cơ bản:

- Xác định các thành phần của user form
- Lấy thông tin về tỷ giá hối đoái dựa vào ngày được nhập vào form từ Website
- Đưa thông tin lấy được vào trong Excel
- Thực hiện các tính toán
- Vẽ đồ thị

### 9.2. Xác định các thành phần của user form

{{< figure src="userform1.png" width=60% >}}

### 9.3. Lấy dữ liệu từ internet

Trong phần này, chúng ta sẽ thực hiện một số nhiệm vụ gồm:

- Xác định ngày hiện tại và đưa vào DateBox.
- Lấy dữ liệu tỷ lệ hối đoái tương ứng với ngày trong DateBox từ internet.
- Nhập các thông tin tương ứng từ dữ liệu lấy được vào trong ComboBox.

```vbnet
Option Explicit

Sub OpenForm()

' Khai báo
Dim i As Integer
Dim DateArray As Variant
Dim currencies As Worksheet, importedCurrencies As Worksheet
Dim DateBox As Variant
Dim DateDay As Integer, DateMonth As String, DateYear As Integer
Dim url As String

Dim currImp As Variant, currImpTwo As Variant, currImpLabel As Variant, currCopy As Variant
Dim currImpCode As String, currImpName As String

Set currencies = Workbooks("currency-converter.xlsm").Worksheets("Currencies")
Set importedCurrencies = Workbooks("currency-converter.xlsm").Worksheets("Sheet1")

currencies.Select
Range("A1").Select

' Xử lý Date và nhập vào DateBox

DateArray = Split(Now())

UserForm1.DateBox = DateAdd("d", -2, DateArray(0))

DateDay = Day(UserForm1.DateBox)
DateMonth = Month(UserForm1.DateBox)
DateYear = Year(UserForm1.DateBox)

If Len(DateMonth) = 1 Then
    DateMonth = "0" & DateMonth
End If

' Lấy dữ liệu từ Internet

    url = "URL;https://www.xe.com/currencytables/?from=USD&date=" & DateYear & "-" & DateMonth & "-" & DateDay & "#table-section"
    With Worksheets("Sheet1").QueryTables.Add(Connection:=url, Destination:=Worksheets("Sheet1").Range("A1"))
        .Name = "My Query"
        .RowNumbers = False
        .FillAdjacentFormulas = False
        .PreserveFormatting = True
        .RefreshOnFileOpen = False
        .BackgroundQuery = False
        .RefreshStyle = xlOverwriteCells
        .SavePassword = False
        .SaveData = True
        .AdjustColumnWidth = True
        .RefreshPeriod = 0
        .WebSelectionType = xlEntirePage
        .WebFormatting = xlWebFormattingNone
        .WebPreFormattedTextToColumns = True
        .WebConsecutiveDelimitersAsOne = True
        .WebSingleBlockTextImport = False
        .WebDisableDateRecognition = False
        .WebDisableRedirections = False
        .Refresh BackgroundQuery:=False
    End With

' Lọc thông tin và đưa vào sheet currencies

For Each currImp In importedCurrencies.Range("A:A")
    If Len(currImp) = 3 Then
        currImpCode = currImp.Value
        currImpName = currImp.Offset(0, 1).Value
            For Each currCopy In currencies.Range("A:A")
                If currCopy = currImpCode And currCopy <> "USD" Then
                    Exit For
                ElseIf currCopy = currImpCode And currCopy = "USD" Then
                    currCopy.Offset(0, 1).Value = "US Dollar"
                    Exit For
                ElseIf currCopy = "" Then
                    currCopy.Value = currImpCode
                    currCopy.Offset(0, 1).Value = currImpName
                    Exit For
                End If
            Next
    ElseIf currImp.Offset(1, 0).Value = "" And currImp.Offset(2, 0).Value = "" _
           And currImp.Offset(3, 0).Value = "" And currImp.Offset(4, 0).Value = "" Then
        Exit For
    End If
Next

' Nhập thông tin vào trong Combobox

For i = 1 To WorksheetFunction.CountA(Columns("A:A"))
    UserForm1.ConvFromBox.AddItem ActiveCell.Offset(i - 1, 0) & " - " & ActiveCell.Offset(i - 1, 1)
Next i

For i = 1 To WorksheetFunction.CountA(Columns("A:A"))
    UserForm1.ConvToBox.AddItem ActiveCell.Offset(i - 1, 0) & " - " & ActiveCell.Offset(i - 1, 1)
Next i

UserForm1.ConvFromBox.Text = Range("A1") & " - " & Range("B1")
UserForm1.ConvToBox.Text = Range("A1") & " - " & Range("B1")
UserForm1.Show
End Sub
```

### 9.4. Thực hiện chuyển đổi tiền tệ

```vbnet

Private Sub ConvertBotton_Click()

' Khai báo
Dim currencies As Worksheet, importedCurrencies As Worksheet
Dim DateArray As Variant
Dim DateDay As String, DateMonth As String, DateYear As String
Dim url As String
Dim Exists As Boolean
Dim currImp As Variant, currImpTwo As Variant, currImpLabel As Variant, currCopy As Variant
Dim currImpCode As String, currImpName As String
Dim initAmt As Double, convAmt As Double
Dim convFrom As String, convFromName As String, convTo As String, convToName As String
Dim initAmtUnit As String, convToUnit As String
Dim testVar As String
Dim currentDate As String
Dim currYear As Integer

Set currencies = Workbooks("currency-converter.xlsm").Worksheets("Currencies")
Set importedCurrencies = Workbooks("currency-converter.xlsm").Worksheets("Sheet1")

Application.ScreenUpdating = False
importedCurrencies.Visible = True

'SAVE CURRENT YEAR

DateArray = Split(Now())
currentDate = DateArray(0)
currYear = Year(currentDate)

'ERROR CHECKING AND DATE ACQUISITION

If UserForm1.AmtBox = "" Then MsgBox ("Input cannot be blank. "): GoTo Reset
If Not IsNumeric(UserForm1.AmtBox) Then MsgBox ("Value must be a number."): GoTo Reset
If UserForm1.AmtBox <= 0 Then MsgBox ("Please enter a positive number."): GoTo Reset
If DateBox = "" Then MsgBox ("Date cannot be empty."): GoTo Reset
If Not IsDate(DateBox) Then MsgBox ("Incorrect date format."): GoTo Reset

DateDay = Day(DateBox)
DateMonth = Month(DateBox)
DateYear = Year(DateBox)

If Len(DateDay) = 1 Then DateDay = "0" & DateDay
If Len(DateMonth) = 1 Then DateMonth = "0" & DateMonth
If Len(DateYear) < 4 Then MsgBox ("Incorrect year length."): GoTo Reset
If DateYear > currYear Then MsgBox ("Year cannot exceed current year."): GoTo Reset

'IMPORT CURRENCY INFORMATION

    url = "URL;https://www.xe.com/currencytables/?from=USD&date=" & DateYear & "-" & DateMonth & "-" & DateDay & "#table-section"
    With Worksheets("Sheet1").QueryTables.Add(Connection:=url, Destination:=Worksheets("Sheet1").Range("A1"))
        .Name = "My Query"
        .RowNumbers = False
        .FillAdjacentFormulas = False
        .PreserveFormatting = True
        .RefreshOnFileOpen = False
        .BackgroundQuery = False
        .RefreshStyle = xlOverwriteCells
        .SavePassword = False
        .SaveData = True
        .AdjustColumnWidth = True
        .RefreshPeriod = 0
        .WebSelectionType = xlEntirePage
        .WebFormatting = xlWebFormattingNone
        .WebPreFormattedTextToColumns = True
        .WebConsecutiveDelimitersAsOne = True
        .WebSingleBlockTextImport = False
        .WebDisableDateRecognition = False
        .WebDisableRedirections = False
        .Refresh BackgroundQuery:=False
    End With

'IMPORT/UPDATE CURRENCIES LIST INTO CURRENCIES SHEET

For Each currImp In importedCurrencies.Range("A:A")
    If Len(currImp) = 3 Then
        currImpCode = currImp.Value
        currImpName = currImp.Offset(0, 1).Value
            For Each currCopy In currencies.Range("A:A")
                If currCopy = currImpCode And currCopy <> "USD" Then
                    Exit For
                ElseIf currCopy = currImpCode And currCopy = "USD" Then
                    currCopy.Offset(0, 1).Value = "US Dollar"
                    Exit For
                ElseIf currCopy = "" Then
                    currCopy.Value = currImpCode
                    currCopy.Offset(0, 1).Value = currImpName
                    Exit For
                End If
            Next
    ElseIf currImp.Offset(1, 0).Value = "" And currImp.Offset(2, 0).Value = "" _
           And currImp.Offset(3, 0).Value = "" And currImp.Offset(4, 0).Value = "" Then
        Exit For
    End If
Next

'CONVERT SELECTED CURRENCY

    initAmt = UserForm1.AmtBox.Value
    convFrom = Left(UserForm1.ConvFromBox, 3)
    convFromName = Right(UserForm1.ConvFromBox, Len(UserForm1.ConvFromBox) - 6)
    convTo = Left(UserForm1.ConvToBox, 3)
    convToName = Right(UserForm1.ConvToBox, Len(UserForm1.ConvToBox) - 6)
    For Each currImp In importedCurrencies.Range("A:A")
        If currImp = convFrom And currImp.Offset(0, 1).Value = convFromName Then
            initAmtUnit = currImp.Offset(0, 2).Value
            For Each currImpTwo In importedCurrencies.Range("A:A")
                If currImpTwo = convTo And currImpTwo.Offset(0, 1).Value = convToName Then
                    convToUnit = currImpTwo.Offset(0, 2).Value
                    UserForm1.FinalAmtBox.Text = Round(initAmt * (convToUnit / initAmtUnit))
                    GoTo Reset:
                End If
            Next
        End If
    Next

Reset:
Sheets("Sheet1").Visible = False
Application.ScreenUpdating = True

End Sub
```

### 9.5. Vẽ đồ thị

```vbnet
Private Sub PlotBotton_Click()

Dim TodaysDate As String
Dim SelectedCurrency As String
Dim i As Integer
Dim url As String
Dim plotVar As Variant
Dim plotData As Worksheet, importedCurrencies As Worksheet
Dim DateArray As Variant
Dim currentDate As String
Dim currYear As Integer
Dim DateDay As String, DateMonth As String, DateYear As String
Dim currImp As Variant, currImpTwo As Variant, currImpLabel As Variant, currCopy As Variant
Dim currImpCode As String, currImpName As String
Dim initAmt As Double, convAmt As Double
Dim convFrom As String, convFromName As String, convTo As String, convToName As String
Dim initAmtUnit As String, convToUnit As String
Dim Chart6 As ChartObject

Application.ScreenUpdating = False

Set importedCurrencies = Workbooks("currency-converter.xlsm").Worksheets("Sheet1")
Set plotData = Workbooks("currency-converter.xlsm").Worksheets("PlotData")

plotData.Visible = True
importedCurrencies.Visible = True

If UserForm1.AmtBox = "" Then MsgBox ("Input cannot be blank. "): GoTo ErrorReset
If Not IsNumeric(UserForm1.AmtBox) Then MsgBox ("Value must be a number."): GoTo ErrorReset
If UserForm1.AmtBox <= 0 Then MsgBox ("Please enter a positive number."): GoTo ErrorReset

plotData.Select: Range("A30").Select

TodaysDate = UserForm1.DateBox.Value
SelectedCurrency = Left(UserForm1.ConvFromBox, 3)

'SAVE CURRENT YEAR

DateArray = Split(Now())
currentDate = DateArray(0)
currYear = Year(currentDate)

'ERROR CHECKING AND DATE ACQUISITION

If UserForm1.AmtBox = "" Then MsgBox ("Input cannot be blank. "): GoTo ErrorReset
If Not IsNumeric(UserForm1.AmtBox) Then MsgBox ("Value must be a number."): GoTo ErrorReset
If UserForm1.AmtBox <= 0 Then MsgBox ("Please enter a positive number."): GoTo ErrorReset
If DateBox = "" Then MsgBox ("Date cannot be empty."): GoTo ErrorReset
If Not IsDate(DateBox) Then MsgBox ("Incorrect date format."): GoTo ErrorReset

DateDay = Day(DateBox)
DateMonth = Month(DateBox)
DateYear = Year(DateBox)

If Len(DateDay) = 1 Then DateDay = "0" & DateDay
If Len(DateMonth) = 1 Then DateMonth = "0" & DateMonth
If Len(DateYear) < 4 Then MsgBox ("Incorrect year length."): GoTo ErrorReset
If DateYear > currYear Then MsgBox ("Year cannot exceed current year."): GoTo ErrorReset

'CALCULATE 30 DAYS PRIOR TO SELECTED DATE
For i = 30 To 1 Step -1
    Range("A" & 30 - i + 1) = DateAdd("d", -i + 1, TodaysDate)
Next i

'IMPORT CURRENCY INFORMATION BASED OFF DATE INFORMATION ABOVE

For Each plotVar In Sheets("PlotData").Range("A:A")

    DateDay = Day(plotVar)
    DateMonth = Month(plotVar)
    DateYear = Year(plotVar)

    If Len(DateDay) = 1 Then DateDay = "0" & DateDay
    If Len(DateMonth) = 1 Then DateMonth = "0" & DateMonth

'IMPORT CURRENCY INFORMATION

    url = "URL;https://www.xe.com/currencytables/?from=USD&date=" & DateYear & "-" & DateMonth & "-" & DateDay & "#table-section"
    With Worksheets("Sheet1").QueryTables.Add(Connection:=url, Destination:=Worksheets("Sheet1").Range("A1"))
        .Name = "My Query"
        .RowNumbers = False
        .FillAdjacentFormulas = False
        .PreserveFormatting = True
        .RefreshOnFileOpen = False
        .BackgroundQuery = False
        .RefreshStyle = xlOverwriteCells
        .SavePassword = False
        .SaveData = True
        .AdjustColumnWidth = True
        .RefreshPeriod = 0
        .WebSelectionType = xlEntirePage
        .WebFormatting = xlWebFormattingNone
        .WebPreFormattedTextToColumns = True
        .WebConsecutiveDelimitersAsOne = True
        .WebSingleBlockTextImport = False
        .WebDisableDateRecognition = False
        .WebDisableRedirections = False
        .Refresh BackgroundQuery:=False
    End With

'CONVERT SELECTED CURRENCY

    initAmt = UserForm1.AmtBox.Value
    convFrom = Left(UserForm1.ConvFromBox, 3)
    convFromName = Right(UserForm1.ConvFromBox, Len(UserForm1.ConvFromBox) - 6)
    convTo = Left(UserForm1.ConvToBox, 3)
    convToName = Right(UserForm1.ConvToBox, Len(UserForm1.ConvToBox) - 6)
    For Each currImp In importedCurrencies.Range("A:A")
        If currImp = convFrom And currImp.Offset(0, 1).Value = convFromName Then
            initAmtUnit = currImp.Offset(0, 2).Value
            For Each currImpTwo In importedCurrencies.Range("A:A")
                If currImpTwo = convTo And currImpTwo.Offset(0, 1).Value = convToName Then
                    convToUnit = currImpTwo.Offset(0, 2).Value
                    plotVar.Offset(0, 1) = initAmt * (convToUnit / initAmtUnit)
                    GoTo Reset:
                End If
            Next
        End If
    Next

Reset:

If plotVar.Offset(1, 0).Value = "" Then
    Exit For
End If

Next

'PLOT DATA ON A GRAPH

Sheets("Last 30 Days").Select
ActiveSheet.ChartObjects("Chart 1").Activate
ActiveChart.ChartTitle.Select
ActiveChart.ChartTitle.Text = "Last 30 Days: " & UserForm1.ConvFromBox & " to " & UserForm1.ConvToBox

ErrorReset:

importedCurrencies.Visible = False
plotData.Visible = False
Worksheets("Currencies").Select
Application.ScreenUpdating = True

End Sub
```

### 9.6. Xử lý ExitButton

```vbnet
Private Sub ExitBotton_Click()
Unload UserForm1
End Sub
```

### 9.7. Kết quả

Cuối cùng thì, đây là file kết quả: [Currency Converter](currency-converter.xlsm). Còn dưới đây là một ví dụ khi chạy chương trình:

{{< figure src="plot-last-30days.png" >}}
