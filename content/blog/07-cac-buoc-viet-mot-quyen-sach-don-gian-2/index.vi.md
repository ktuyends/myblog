---
title: "Các bước viết một quyển sách nho nhỏ (phần 2)"
subtitle: ""
slug: jupyter-book
summary: "Trong [bài viết](/blog/01-blog/writing-a-book-with-bookdown/) trước, tôi đã viết về `bookdown`, một packages giúp viết sách sử dụng R Markdown. Nếu bạn là một người hay sử dụng Python, có thể bạn sẽ thích sử dụng Jupyter hơn là R Markdown,..."
date: 2021-10-20
lastmod: 2021-10-20
draft: false
authors: ["Tuyen Kieu"]
images: ["featured.png"]
tags: ["Blog"]
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

Trong [bài viết](/writing-a-book-with-bookdown/) trước, tôi đã viết về `bookdown`, một packages giúp viết sách sử dụng R Markdown. Nếu bạn là một người hay sử dụng Python, có thể bạn sẽ thích sử dụng Jupyter hơn là R Markdown,...Thật may mắn là trong Python chúng ta cũng có một thư viện tương tự như `bookdown`, là `jupyter book`.

Jupyter Book là một dự án mã nguồn mở, vẫn đang trong quá trình xây dựng các tính năng, tuy nhiên với những tính năng hiện tại về cơ bản cũng đủ để chúng ta có thể tạo ra được những quyển sách có hình thức đẹp, dựa trên các files jupyter `.ipynb`.

## 1. Các bước tạo một quyển sách đơn giản

### 1.1. Cài đặt các thư viện

```python
# Cài đặt jupyter-book
conda install jupyter-book

# Cài đặt ghp-import để tạo nhánh gh-page
conda install ghp-import
```

### 1.2. Tạo sách

Sau khi đã cài đặt `jupyter-book` và `ghp-import` ta sẽ có quy trình như sau:

```bash
# Tạo sách (jb hoặc jupyter-book đều được)
jb create path/book_name

# build sách
cd book_name
jb build .
```

### 1.3. Cấu trúc của một quyển sách 

Sau khi chạy các lệnh trên, một số tập tin và thư mục đã được tạo ra:

```
├── _build/
├── _config.yml
├── _toc.yml
├── files.md
├── files.ipynb
├── requirements.txt
├── ref.bib
└── _static
    └── myfile.css
```

Trong đó:

- `_build`: Thư mục chứa các files sau khi build. Để xem sách, ta mở file: `_build/html/index.html`
- `_config.yml`: Cấu hình sách
- `_toc.yml`: Mục lục và thứ tự sắp xếp các file nội dung
- `.md` và `.ipynb`: Các file chứa nội dung quyển sách
- `_static/myfile.css`: Tùy chỉnh font, màu sắc,...
- `requirements.txt`: Thông tin về các thư viện được sử dụng
- `ref.bib`: Thông tin về tài liệu tham khảo
### 1.4. Publish

Tôi sử dụng Github để lưu trữ quyển sách của mình, sau đó sử dụng Github pages để publish sách. 

Đầu tiên cần tạo Repository trên Github cho quyển sách, sau đó vào thư mục quyển sách ở trên máy tính chạy các lệnh sau:

```bash
# khởi tạo local repository
git init
git branch -M main

# liên kết với remote
git remote add origin url/repo_name.git
```

Bây giờ, ta đã liên kết quyển sách ở trên máy tính với Github. Quy trình tiếp theo sẽ như sau:

```bash
# chỉnh sửa và build lại sách
jb build .

# tạo gh-pages
ghp-import -n -p -f _build/html

# push
git add .
git commit -m "commit_msg"
git push -u origin main
```

Khi đó, ta sẽ có một quyển sách ở địa chỉ: `http(s)://github_id.github.io/book_repository/`

## 2. Tùy chỉnh một số thành phần

### 2.1. File `_config.yml`

File `_config.yml` là file cấu hình quyển sách, gồm rất rất nhiều thông tin như chú thích bên dưới:

```yml
# Book settings
title:   # The title of the book
author:   # The author of the book to be placed in the footer
logo: ./figures/logo.png  # A path to the book logo

# Execute
execute:

# HTML-specific settings
html:
  favicon: ./figures/favicon-32x32.png  # A path to a favicon image
  navbar_footer_text: Visit our <a href="url">GitHub
    Repository</a> <div> This book is powered by <a href="https://jupyterbook.org">Jupyter
    Book</a> </div>  # Will be displayed underneath the left navigation bar.
  home_page_in_navbar: false  # Whether to include your home page in the left Navigation Bar
  use_repository_button: true  # Whether to add a link to your repository button
  use_issues_button: true  # Whether to add an "open an issue" button
  comments:
    utterances:
      repo: "github-org/github-repo"  

# Launch button settings
repository:
  url:  # The URL to your book's repository
  branch: main  # Which branch of the repository should be used when creating links (optional)

# Add a bibtex file so that we can create citations
bibtex_bibfiles:
  - references.bib

# bib style
sphinx:
  config:
    bibtex_reference_style: author_year
    html_show_copyright: false
    html_js_files:
    - https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.4/require.min.js  
    mathjax_path: https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js
parse:
  myst_enable_extensions:
    # don't forget to list any other extensions you want enabled,
    # including those that are enabled by default!
    - amsmath
    - dollarmath
```

### 2.2. File `_toc.yml`

File `_toc.yml` sắp xếp các file nội dung theo một thứ tự nào đó. Ví dụ:

```yml
format: jb-book
root: index
parts:
  - caption: Name of Part 1
    numbered: True
    maxdepth: 2
    chapters:
    - file: path/to/part1/chapter1
    - url: https://example.com
      title: Example website
    - file: path/to/part1/chapter2
      sections:
      - file: path/to/part1/chapter2/section1
  - caption: Name of Part 2
    chapters:
    - file: path/to/part2/chapter1
    - file: path/to/part2/chapter2
      sections:
      - file: path/to/part2/chapter2/section1
```

Trong đó:

- `root`: Trang đầu tiên của quyển sách
- `parts -> caption`: Tên các phần, nếu quyển sách chia thành từng phần
- `chapters` và `sections`: Các chương của sách, mỗi file tương ứng một chương hoặc một phần của chương
- `title`: Tiêu đề thay thế tiêu đề chapters, sections
- `maxdepth`: Số levels hiển thị ở mục lục
- `numbered`: Có đánh số tiêu đề hay không

### 2.3. File `requirements.txt`

File `requirements.txt` chứa thông tin về các thư viện chúng ta sử dụng trong quyển sách. Ví dụ:

```
graphviz=0.16
jupyter=1.0.0
jupyter-book=0.10.2
matplotlib=3.2.2
numpy==1.18.5
pandas==1.0.5
pandarallel==1.5.1
pip==20.1.1
python==3.8.3
seaborn==0.10.1
Sphinx==3.5.2
sphinxcontrib-bibtex==2.1.4
xgboost=1.3.3
```

## 3. Viết bài

Trong phần này, tôi chỉ tóm tắt lại một số nội dung mình hay sử dụng. Chi tiết hơn các bạn có thể tham khảo trong các bài sau:

- [Write narrative content](https://jupyterbook.org/content/index.html)
- [Write executable content](https://jupyterbook.org/content/executable/index.html)
- [MyST syntax cheat sheet](https://jupyterbook.org/reference/cheatsheet.html)

### 3.1. Blocks

````
# Tạo một note, warning
```{note}
Here is a note!
```

# admonition, :class: là các tùy chọn
```{admonition} Here's your admonition
:class: tip
Here's the admonition content
```

# sidebar
```{sidebar} My sidebar title
My sidebar content
```

```{margin} An optional title
My margin content
```
````

### 3.2. Citations và bibliographies

Để sử dụng các trích dẫn tài liệu tham khảo, ta cần có một file bibtex - `file_name.bib` sau đó thêm các dòng sau vào trong file `_config.yml`:

```yml
# Add a bibtex file so that we can create citations
bibtex_bibfiles:
  - file_name.bib

sphinx:
  config:
    bibtex_reference_style: author_year
```

Để trích dẫn, sử dụng cú pháp: `` {cite:ps}`key` ``

Để tạo bibliographies sử dụng câu lệnh sau ở cuối bài viết hoặc cuối quyển sách:

````
```{bibliography}
:filter: docname in docnames
```
````

### 3.3. Công thức toán học

Jupyter Book sử dụng Mathjax để viết công thức toán học. Phiên bản hiện tại hình như là phiên bản 2, nếu chúng ta muốn sử dụng phiên bản 3 thì cần phải cấu hình một chút trong file `_config.yml` như sau:

```yml
sphinx:
  config:
    mathjax_path: https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js
```

Để viết các công thức toán học bên trong đoạn văn, ta sử dụng `$math_express$` ở vị trí cần chèn.

Để viết các công thức toán học trên một dòng riêng biệt, ta sử dụng:

```
# Sử dụng (my_label) nếu muốn đánh số phương trình để sau tham chiếu
# Sử dụng {eq}`my_label` để tham chiếu

$$
math_express
$$ (my_label)
```

Mathjax mặc dù hỗ trợ rất nhiều trong việc viết công thức toán học, nhưng vẫn không được đầy đủ như LaTex. Ta cấu hình thêm một chút để Jupyter Book hỗ trợ thêm:

```yml
# Trong file _config.yml
parse:
  myst_enable_extensions:
    # don't forget to list any other extensions you want enabled,
    # including those that are enabled by default!
    - amsmath
    - dollarmath    
```

### 3.4. Hình ảnh

**Images:**

Cú pháp chèn hình ảnh của Markdown cơ bản: `![img_text](path/to/img)`

Cú pháp chèn hình ảnh của MyST Markdown:

````
```{image} path/to/img
:alt: 
:class: 
:width: 
:align: 
```
````

**Figures:**

Figures tương tự như images, nhưng nó bao gồm nhiều thông tin hơn và có thể tham chiếu:

````
# name dùng để tham chiếu, sử dụng cú pháp: {ref}`name_text`

```{figure} path/to/fig
---
scale:
width: 
height:
alt:
align: 
name: 
---
Caption!
```
````

Một số cách tham chiếu:

- ``{ref}`name_text` ``
- ``{ref}`New Lable <name_text>` ``
- ``{numref}`name_text` ``
- ``{numref}`Figure {number}: {name} <name_text>` ``

---