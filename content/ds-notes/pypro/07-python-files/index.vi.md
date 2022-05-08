---
title: "Pypro - Python Files"
subtitle: ""
slug: python-files
date: 2022-03-05
lastmod: 2022-03-05
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
series: [Python Programming]
series_weight: 7
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
## 1. Mở và đóng file

### 1.1. Mở file

Trước khi muốn làm việc với một file, ta cần phải mở file đó. Trong Python, hỗ trợ hàm `open()` để mở file và sẽ trả về một đối tượng file. Loại của đối tượng sẽ phụ thuộc vào chế độ `mode` khi file được mở, và với mỗi đối tượng file sẽ có hai phương thức là `read()` và `write()`. Cú pháp:

```python
file = open("test_file.txt","w+")
file.read()
file.write("a new line")
```

Các chế độ mode cơ bản khi mở file:

|Mode| Ý nghĩa |
|-|-|
| r | Mở file với chế độ đọc|
| r+ | Mở file với chế độ đọc và viết, con trỏ ở đầu file |
| w | Mở file với chế độ viết, nếu file tồn tại sẽ bị ghi đè |
| w+ | Mở file với chế độ đọc và viết, nếu file tồn tại sẽ bị ghi đè |
| a | Mở file ở chế độ viết, con trỏ ở cuối file, thêm nội dung vào cuối file nếu nó tồn tại |

### 1.2. Đóng file

Sau khi đã hoàn thành công việc với các file, chúng ta nên đóng nó lại với hàm `close()`. Nếu không, có thể có một số hành vi mà chúng ta không thể dự đoán trước được sẽ xảy ra.

Cách 1: Sử dụng trực tiếp hàm `close()`

```python
try:
    file = open("test_file.txt","w+")
    file.write("a new line")
except Exception as e:
    logging.exception(e)
finally:
    file.close()
```

Cách 2: Sử dụng context manager với with:

```python
with open("test_file.txt", "w+") as file:
    file.write("a new line)
```

Câu lệnh này sẽ tự động đóng file khi chúng ta hoàn tất công việc.

## 2. Đọc và viết file

### 2.1. Đọc file

Sau khi mở file, bước tiếp theo bạn có thể muốn đọc hoặc là viết nội dung vào file. Để đọc một file, Python cung cấp cho chúng ta ba lựa chọn: 

- _read()_: Trả về toàn bộ nội dung của file.
- _readline()_: Trả về một dòng bao gồm ký tự `\n` ở cuối dòng. Nó sẽ đọc từng dòng một.
- _readlines()_: Trả về tất cả các dòng trong file ở dạng list.

### 2.2. Viết file

Khác với đọc file, viết file chỉ có hai lựa chọn:

- _write(str)_: Viết một chuỗi vào file.
- *writelines(list_line)*: Viết một list các dòng vào file, người viết chương trình phải có nhiệm vụ thêm `\n` vào cuối dòng.


## 3. File và file path

### 3.1. Pathlib

Một file, về cơ bản sẽ có hai thuộc tính: Tên file và file path (đường dẫn đến file). Tên file lại bao gồm hai thành phần là phần tên và phần mở rộng. Để làm việc với các file, ta sẽ sử dụng module _pathlib_.



```python
# Load module
from pathlib import Path

# Tạo file path
Path("Andy", "Learnds", "Python")
```




    WindowsPath('Andy/Learnds/Python')




```python
# Giả sử ta có nhiều file trong một folder nào đó
my_files = ['accounts.txt', 'details.csv', 'invite.docx']
for filename in my_files:
    print(Path(r'C:\Users\LearnDS', filename))
```

    C:\Users\LearnDS\accounts.txt
    C:\Users\LearnDS\details.csv
    C:\Users\LearnDS\invite.docx
    


```python
# Toán tử '/' dùng để nối Path
Path('C:/') / 'User' / 'Andy' / 'LearnDS' 
```




    WindowsPath('C:/User/Andy/LearnDS')




```python
## Home and working directory
print(f'Home directory: {Path.home()}')
print(f'Working directory: {Path.cwd()}')
```

    Home directory: C:\Users\ktuyends
    Working directory: d:\Andy\myblog\content\ds-notes\pypro\07-python-files
    

### 3.2. Relative và absolute

Có hai cách để biểu diễn đường dẫn đến file trong Python:

- Đường dẫn tuyệt đối: luôn bắt đầu bằng thư mục root.
- Đường dẫn tương đối: bắt đầu bằng working directory.

{{< figure src="./file-path.jpg" >}}

**Tạo directory**

```python
# Cú pháp cơ bản:
path = Path("parentdirectory/mydirectory")
path.mkdir(parents = True, exist_ok = True)

# Trong trường hợp filepath chứa tên file 
# Sử dụng parent nếu không nó sẽ lấy tên file làm tên directory
path.parent.mkdir(parents = True, exist_ok = True)
```

**Một số hàm kiểm tra**

```python
path.exists() # True nếu path tồn tại
path.is_file() # True nếu path tham chiếu đến file
path.is_dir() # True nếu path tham chiếu đến thư mục
path.is_absolute() # True nếu path là tuyệt đối
```

### 3.3. Các phần của filepath

{{< figure src="./file-path2.jpg" >}}

Một số phương thức trích xuất các phần của file:

```python
# filepath
p = Path('C:/Users/Al/spam.txt')

# Parts of filepath
p.anchor # Root folder
p.parent # parent directory
p.name   # spam.txt
p.stem   # spam
p.suffix # .txt
```

### 3.4. Tìm kiếm files

Glob được sử dụng để tìm kiếm và làm việc với nhiều file, directory.

```python
# filepath
p = Path('C:/Users/Al/Desktop')

# Danh sách tất cả các file
# * đại diện cho một hoặc nhiều ký tự 
# ? đại diện cho một ký tự đơn
p.glob('*') # Generator
list(p.glob('*'))

# Danh sách các file txt
list(p.glob('*.txt'))

# Tìm kiếm các file bao gồm các file trong thư mục con
# ** mang ý nghĩa tìm kiếm đệ quy
p.glob('**/*.txt')

# Tìm kiếm các thư mục đệ quy
p.glob('**/*')
```



### 3.5. Đọc và viết file

```python
# Viết file, ghi đè lên tệp hiện tại
p = Path('spam.txt')
p.write_text('Hello, world!')

# Đọc file
p.read_text()

# Viết file, thêm dữ liệu vào file
with p.open("a") as f:
    f.write("Do something!")
```

## 4. Shutil module

Module shutil là module chứa nhiều hàm thực hiện các thao tác như copy, move, rename,...Thường được kết hợp với pathlib khi xử lý các files.

### 4.1. Copy files và folders

```python
# Cú pháp cơ bản
# source: filepath của file hiện tại
# destination: filepath của nơi bạn muốn copy, 
# shutil.copy chỉ copy một single file

shutil.copy(source, destination)

# Ví dụ
import shutil
from pathlib import Path
p = Path.home()
shutil.copy(p / 'spam.txt', p / 'some_folder')

# Nếu destination là file name nó sẽ là tên mới của file được copy
shutil.copy(p / 'eggs.txt', p / 'some_folder/eggs2.txt')

# Copy toàn bộ file và thư mục con trong một thư mục
# shutil.copytree(source, destination)
shutil.copytree(p / 'spam', p / 'spam_backup')
```


### 4.2. Move và rename

Cú pháp:

```python
# shutil.move(source, destination)
# Di chuyển các files hoặc folder ở source vào destination
# Nếu destination là folder, sẽ di chuyển vào bên trong folder
# Nếu tồn tại file trong thư mục destination, move sẽ ghi đè
shutil.move('C:\\bacon.txt', 'C:\\eggs') # C:\\eggs\\bacon.txt

# Nếu destination là tên file, nó sẽ là tên mới của file move
shutil.move('C:\\bacon.txt', 'C:\\eggs\\new_bacon.txt') # C:\\eggs\\new_bacon.txt

# Nếu không tìm thấy tên folder trong destination nó sẽ tưởng đầy là tên file và đổi tên
```

### 4.3. Delete file

Cú pháp:

```python
# Xóa file
from pathlib import Path
file_path = Path('/tmp/file.txt')
file_path.unlink() 

# Xóa thư mục rỗng
dir_path = Path('/tmp/img')
dir_path.rmdir()

# Xóa thư mục có chứa các file
dir_path = Path('/tmp/img')
shutil.rmtree(dir_path)
```
