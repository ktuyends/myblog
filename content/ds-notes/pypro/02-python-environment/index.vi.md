---
title: "Pypro - Python environment"
subtitle: ""
slug: python-environment
date: 2021-12-22
lastmod: 2021-12-22
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Programming"]
categories: []
series: [Python Programming]
series_weight: 2
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

<!--more-->
## 1. Cài đặt Windows Terminal và tùy chỉnh

Cách cài đặt thì đơn giản rồi, các bạn vào [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701), sau đó chọn install là xong.

Sau khi cài đặt xong, bật Windows Terminal lên và cài đặt các module sau nếu muốn tùy chỉnh giao diện:

```bash
# Cài đặt Module
Install-Module oh-my-posh -Scope CurrentUser
Install-Module posh-git -Scope CurrentUser

# Xem danh sách các theme
Get-PoshThemes

# Cài đặt và thay đổi theme: CaskaydiaCove NF sau đó
# Thử thay đổi theme
Set-PoshPrompt -Theme theme_name

# Tạo file Profile để lưu thay đổi
notepad $PROFILE

# Nội dung file Profile
Import-Module oh-my-posh
Set-PoshPrompt -Theme paradox
Import-Module posh-git
```

Làm mờ giao diện bằng Transparency, ta mở Setting, sau đó mở file setting.json và sửa:

```bash
"defaults":
{
    // Put settings here that you want to apply to all profiles.
    "useAcrylic": true,
    "acrylicOpacity": 0.7
}
```

## 2. Tạo môi trường với Conda

Đầu tiên, các bạn vào trang [Miniconda](https://docs.conda.io/en/latest/miniconda.html), download và cài đặt phiên bản tương ứng với máy tính.

Sau khi cài đặt xong cần thêm Miniconda vào Path, với Windows thì link sẽ là: `C:\Users\ktuyends\miniconda3\Scripts`

Bật Window PowerShell lên và chạy các lệnh sau để thêm Conda và update:

```bash
conda init
conda config --set auto_activate_base false
conda update --all
conda config --add channels conda-forge
```

### Một số câu lệnh làm việc với môi trường bằng Conda

```bash
# Tạo
conda create -n env_name python=<version>

# Activate
conda activate env_name

# deactivate
conda deactivate

# Xem list
conda info --env

# Xóa
conda remove --name envname --all

# Clone từ myenv
conda create --name myclone --clone myenv

# export
conda active env_name
conda env export > environment.yaml
conda env create -f environment.yaml # từ env khác
```

### Tìm kiếm, cài đặt và xóa package bằng Conda

```bash
# Tìm package
conda search pack_name

# Cài đặt
conda install pack_name=<version>

# Xóa
conda remove pack_name
```

## 3. Quản lý Package với PIP

### Một số câu lệnh PIP

```bash
# Xem danh sách các packages được cài đặt
pip list


# Cài đặt package
pip install pack_name

# Xóa package 
pip uninstall pack_name

# Update 
pip install -U pack_name

# Xem một package được cài đặt ở đâu
pip show pack_name

# Cài đặt pack_age cho một phiên bản Python nào đó
python3 -m pip install pack_name
```

### Danh sách các package được cài đặt

```bash
# Xem danh sách các package và phiên bản
python -m pip freeze

# Tạo danh sách file các package
python -m pip freeze > requirements.txt

# Cài đặt trên một môi trường khác
python -m pip install -r requirements.txt
```

## 4. Pyenv và Poetry

Một trong những hướng dẫn đầu tiên khi học Python là hãy tải Python từ trang web của nó và cài đặt trên hệ điều hành của mình. Tuy nhiên, đây không phải là hành động nên thực hiện. 

Khi chúng ta làm việc với nhiều dự án, mỗi dự án lại dựa trên một phiên bản Python và có các package đi kèm khác nhau. Việc thay đổi các phiên bản đôi lúc làm chương trình không thể thực thi như mong muốn. Hoặc đôi khi trên máy của chúng ta có quá nhiều phiên bản Python, chúng ta không biết là phiên bản hiện tại là phiên bản nào, được cài đặt ở đâu. Vì vậy, lời khuyên là mỗi dự án nên dựa trên một phiên bản Python riêng. Và Pyenv ra đời để giúp chúng ta giải quyết vấn đề này.

### Cài đặt Pyenv trên Windows

Đầu tiên chúng ta vào trang web sau: [Pyenv-win](https://github.com/pyenv-win/pyenv-win), tải xuống repository và giải nén. Sau đó bật PowerShell và chạy các lệnh sau:

```bash
# Tạo thư mục .pyenv
mkdir $HOME/.pyenv

# Copy thư mục pyenv-win và file .version sau khi giải nén file tải về vào .pyenv
# Sau đó chạy 3 lệnh sau
[System.Environment]::SetEnvironmentVariable('PYENV',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_HOME',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('path', $env:USERPROFILE + "\.pyenv\pyenv-win\bin;" + $env:USERPROFILE + "\.pyenv\pyenv-win\shims;" + [System.Environment]::GetEnvironmentVariable('path', "User"),"User")

# Đóng powershell và khởi động lại ở chế độ Admin và chạy lệnh sau
Set-ExecutionPolicy unrestricted
```

### Một số câu lệnh với pyenv

```bash
# Xem tất cả các phiên bản có sẵn
pyenv install --list

# Cài đặt một phiên bản
pyenv install <version>

# Xem các phiên bản được cài đặt bởi pyenv
pyenv versions

# Chỉ định global version
pyenv global <version>
```

### Cài đặt Poetry trên Windows

Mở Windows PowerShell và chạy lệnh sau, sau đó đọc thông báo kết quả và thêm đường dẫn cài đặt vào Path của Windows:

```bash
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py -UseBasicParsing).Content | python -

source $HOME/.poetry/env
```

### Kết hợp Poetry và Pyenv

```bash
# Tạo một dự án với Poetry
poetry new my-project

# Xem dự án được tạo ra
cd my-project
ls

# Chỉ định phiên bản Python
pyenv local <version>
poetry env use python

# Cài đặt các package cho Project
poetry add <pack_name>
poetry install
```

```bash
# update các package
poetry update

# Xóa package
poetry remove package_to_remove

# Thêm Project vào Vscode chạy
poetry shell
code .

# Thay đổi phiên bản Python
pyenv install <new_version>
pyenv local <new_version>
poetry env use python
poetry install
poetry shell
code .
```
