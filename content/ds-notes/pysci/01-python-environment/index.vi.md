---
title: "PySci - Python environment"
subtitle: ""
slug: pysci-python-environment
date: 2022-05-16
lastmod: 2022-05-16
draft: false
authors: ["Tuyen Kieu"]
description: ""
images: []
tags: ["Python for DA"]
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
## 1. Cài đặt JupyterLab

Bạn là một người mới đến với Python, mới sử dụng Python để phân tích dữ liệu, thì cách đơn giản và dễ dàng nhất để cài đặt Python và các Package phục vụ cho công việc tính toán khoa học là cài đặt [Anaconda](https://www.anaconda.com/products/distribution). Nếu bạn không biết cách cài đặt thì mình đã tìm cho bạn một video hướng dẫn cài đặt của _Ken Jee_:

{{< youtube C4OPn58BLaU >}}

Sau khi đã cài đặt Anaconda, chúng ta bắt đầu làm quen với JupyterLab. Vậy thì JupyterLab là gì? Hãy xem video này của bạn _Thu Vũ_. 

{{< youtube zai2pLUD9FA >}}

Trong trường hợp bạn xem không hiểu, hoặc không biết tiếng anh thì hãy cài đặt ngay **_eJOY English extension_** (Search google nha) cho trình duyệt của bạn. Nó sẽ giúp bạn dịch sub của video từ tiếng anh sang tiếng việt đấy.

Và cuối cùng là một video hướng dẫn sử dụng JupyterLab, vẫn là một video từ Youtube. Ôi mình lười viết phần này quá, không thú vị chút nào, haha!

{{< youtube 7wfPqAyYADY >}}





## 2. Cài đặt và sử dụng thư viện

Khi làm việc với Python, nhiều khi chúng ta phải sử dụng các thư viện bên ngoài tùy vào mục đích sử dụng của chúng ta. Ví dụ làm việc với dữ liệu thì cần phải có các thư viện như _numpy, pandas, matplotlib,..._

Để cài đặt thư viện, có hai cách: một là sử dụng PIP, và hai là sử dụng Conda _(Khi cài đặt Anaconda hoặc Miniconda sẽ có)_. Và cả hai lệnh này đều chạy trên môi trường Terminal _(Mac, Linux)_ hoặc Bash, PowerShell, CMD _(với Windows)_.

### 2.1. Sử dụng PIP

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

# Cài đặt package cho một phiên bản Python nào đó
python3 -m pip install pack_name
```

```bash
# Xem danh sách các package và phiên bản
python -m pip freeze

# Tạo danh sách file các package
python -m pip freeze > requirements.txt

# Cài đặt trên một môi trường khác
python -m pip install -r requirements.txt
```

### 2.2. Sử dụng Conda

```bash
# Tìm package
conda search pack_name

# Cài đặt
conda install pack_name=<version>

# Xóa
conda remove pack_name
```

### 2.3. Import packages

Trước khi muốn sử dụng một package, ta phải `import` nó vào trong môi trường của Python. Có hai trường hợp như sau.

**Trường hợp 1: import tên module**

```python
# Import module_name
# Ví dụ:
import math

# Sử dụng các hàm bên trong module math
# math.function_name()
math.pi
math.sqrt(25)
```

```python
# Chúng ta có thể đặt tên mới cho package
# Ví dụ
import numpy as np
import pandas as pd

# Và sử dụng tên mới thay thế cho tên package
np.array([1, 2, 4, 5])
```

**Trường hợp 2: import một hàm cụ thể từ package** 

Trong trường hợp này ta sử dụng trực tiếp tên hàm mà không cần có tiền tố `package_name.` đứng trước nữa.

```python
# ví dụ với module math
from math import pi
print(pi)

# Import toàn bộ 
from math import *
sqrt(25)
```

## 3. Environment (nâng cao)

Khi bạn sử dụng Python được một thời gian dài, làm việc với các dự án khác nhau, có thể bạn sẽ không sử dụng cách cài đặt ở phần 1 nữa mà quan tâm nhiều hơn đến cách quản lý phiên bản của Python và các thư viện được cài đặt cho từng dự án. 

Mình từng viết một bài về [Python environment](/python-environment/) nhưng thực sự nó rất là lằng nhằng và khó hiểu đấy. Bài này mình cũng chỉ đơn giản là tóm tắt lại một số bước cơ bản để thiết lập môi trường việc.

Đầu tiên, với phần này, mình sẽ không quan tâm là laptop của mình đã cài đặt Python hay chưa. Và mình sẽ đi cài đặt lại Python theo một cách khác.

### 3.1. Yêu cầu:

Máy tính của bạn cần cài đặt 3 phần mềm sau:

- [Pyenv](https://github.com/pyenv/pyenv): Quản lý phiên bản cài đặt Python.
- [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv): Quản lý môi trường environment, chỉ sử dụng được với các hệ điều hành hỗ trợ UNIX, nhưng mà mình dùng Windows à, quá buồn.
- [Poetry](https://python-poetry.org/docs/#installation): Quản lý phiên bản của các packages.

### 3.2. Cài đặt Python bằng Pyenv

```bash
# Xem tất cả các phiên bản có sẵn
pyenv install --list

# Cài đặt một phiên bản
pyenv install <version>
pyenv install 3.10.0      # Ví dụ

# Xem các phiên bản Python đã được cài đặt
# Phiên bản đánh dấu * là phiên bản Python đang được sử dụng
pyenv versions

# Chỉ định một phiên bản khác
# set default Python
pyenv global <version>
pyenv global 3.10.0      # Ví dụ
```

### 3.3. Tạo môi trường ảo

Nếu bạn cài đặt được `pyenv-virtualenv` thì có thể sử dụng cú pháp sau:

```bash
# create new virtualenv (e.g. pyenv virtualenv <python-version> <env-name>)
pyenv virtualenv 3.10.0 test_project_env

# activate the virtualenv
pyenv activate test_project_env

# list all available virtual environments
pyenv virtualenvs

# create and navigate to an example directory called 'test_project'
mkdir test_project && cd test_project

# set the 'local' environment to use the 'test_project' virtualenv created above
pyenv local test_project_env
```

Nếu bạn không cài được `pyenv-virtualenv` thì chúng ta có thể sử dụng **_conda_**:

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

Hoặc là sử dụng **_Poetry_**:

```bash
# Tạo một dự án với Poetry
poetry new my-project

# Xem dự án được tạo ra
cd my-project
ls

# Cài đặt phiên bản Python
pyenv install --list
pyenv install <version>
pyenv versions

# Chỉ định phiên bản Python
pyenv local <version>

# Tạo môi trường ảo
poetry env use python

# # Activate environment
poetry shell

# After, run Project in VS Code
code .
```

```bash
# Cài đặt các package cho Project
poetry add <pack_name>

# update các package
poetry update

# Xóa package
poetry remove package_to_remove

# install để cập nhật các thay đổi
poetry install
```

```bash
# Trường hợp thay đổi phiên bản Python
pyenv install <new_version>     # Cài đặt phiên bản mới
pyenv local <new_version>       # Chỉ định phiên bản mới
poetry env use python           # Tạo môi trường ảo
poetry install                  # Update các thay đổi
poetry shell                    # Active environment
code .                          # Run project in vscode
```
