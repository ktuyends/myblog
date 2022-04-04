---
title: "Một vài lưu ý khi cài đặt Ubuntu"
subtitle: ""
slug: install-ubuntu-desktop
summary: "Nếu một ngày nào đó, bạn phải làm một công việc mà không được hỗ trợ bởi Windows, bạn sẽ làm gì? Dĩ nhiên là phải tìm một hệ điều hành khác thay thế cho Windows rồi..."
date: 2016-03-10
lastmod: 2016-03-10
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

Nếu một ngày nào đó, bạn phải làm một công việc mà không được hỗ trợ bởi Windows, bạn sẽ làm gì? Dĩ nhiên là phải tìm một hệ điều hành khác thay thế cho Windows rồi.

Nhưng đang dùng Windows quen, tự nhiên phải chuyển qua một hệ điều hành lạ hoắc thì không dễ chịu chút nào. Những ngày đầu, chuyển qua dùng Linux (Ubuntu), có khá nhiều vấn đề mình phải tìm hiểu lại từ đầu như hệ thống thư mục, cài đặt phần mềm, cấu hình,...Và lúc đầu cài đặt Ubuntu, mình cũng gặp khá nhiều khó khăn.

## 1. Cài đặt Ubuntu

Có nhiều cách để cài đặt một hệ điều hành. Với Ubuntu bạn có thể cài độc lập một hệ điều hành riêng, cài trên máy ảo hoặc cài song song Dual-Boot với các hệ điều hành khác. Để cài đặt Ubuntu, các bạn có thể tìm thấy rất nhiều hướng dẫn, nhưng trực quan nhất là tìm các Tutorial trên Youtube.

Chọn phương thức cài đặt nào là do nhu cầu của mỗi người. Nếu bạn không cần làm gì liên quan đến Windows nữa thì các bạn có thể cài Ubuntu và xóa Windows. Nếu các bạn chỉ muốn vọc vạch Ubuntu cho biết, thì các bạn nên cài đặt thông qua máy ảo. Còn nếu bạn muốn sử dụng cả 2 hệ điều hành, thì Dual-Boot là lựa chọn dành cho bạn. Về phần mình, thì mình chọn Dual-Boot.

Để cài đặt Ubuntu các bạn sẽ cần chuẩn bị 2 thứ.

- Một USB tối thiểu 8GB để làm USB Boot.
- Một [file ISO](https://ubuntu.com/download) cài đặt Ubuntu.

Đối với USB Boot, các bạn sử dụng phần mềm [Rufus](https://rufus.ie/) để tạo Boot.

Có 3 việc, các bạn cần xác định trước khi tạo USB và cài đặt Ubuntu.

- Xác định định dạng của ổ cứng xem nó là MBR hay GPT để tạo USB cho đúng.
- Nếu bạn cài Dual-Boot, thì Windows và Ubuntu phải cùng một định dạng thì mới thành công được. Khuyến khích chuyển tất cả về GPT cho dễ cài đặt.
- Cuối cùng là chuyển đổi Boot của máy tính về định dạng GPT.

Đây là những vấn đề mình đã gặp phải khi cài đặt Ubuntu trong chế độ Dual-Boot, vì không xác định rõ các định dạng trên, làm mình phải cài lại Windows 2-3 lần mới tìm ra nguyên nhân.

## 2. Một số việc phải làm sau khi cài đặt Ubuntu

### 2.1. Đồng bộ giờ giữa Ubuntu và Windows

Mỗi khi khởi lại máy tính, mình phát hiện khi mình vào Ubuntu or khi mình vào Windows, giờ bị đổi múi giờ. Để thực hiện đồng bộ, mình tùy chỉnh trong Ubuntu.

Các bạn mở Terminal lên, gõ câu lệnh sau:

```shell
$ terminal - timedatectl set-local-rtc 1
```

### 2.2. Cài đặt Grub Customize

Grub Customize được sử dụng để chỉnh thứ tự Boot trong Menu khởi động. Mặc định có thể là sẽ Boot thẳng vào Windows hoặc Ubuntu. Nếu bạn muốn đổi lại thứ tự này thì sử dụng Grub Customize. Ứng dụng này có thể tìm thấy trong Ubuntu Software.

### 2.3. Cài đặt Chrome

Mặc định, hệ điều hành Ubuntu đã có Firefox nhưng nếu bạn quen xài Chrome như mình, thì mình nghĩ bạn nên cài đặt nó. Việc cài đặt một số phần mềm trong Ubuntu cũng đơn giản. Bạn chỉ cần vào trang của Chrome và download file cài đặt định dạng `.deb` về mở lên. Click vào Install là nó sẽ tự cài đặt cho bạn.

### 2.4. Cài đặt trình quản lý gói Synaptic Package Manager

Mở Terminal lên nào:

```shell
$ sudo apt-get install synaptic
```

Với Synaptic, việc cài đặt các phần mềm đôi khi sẽ dễ dàng hơn là trong Ubuntu Software.

### 2.5. Tạo tài khoản Root

Root hiểu đơn giản thì nó là cấp quản lý hệ thống cao nhất trong nhất trong Ubuntu. Nó giống như `Run as Administrator` trong Windows vậy. Khi bạn thấy một câu lệnh sử dụng `sudo` nghĩa là nó được áp dụng ở chế độ Root.

Kích hoạt và tạo mật khẩu cho tài khoản Root:

```shell
$ sudo passwd root
```

Để sử dụng trong chế độ root:

```shell
$ su
```

Để kết thúc:

```shell
$ exit
```

### 2.6. Cài đặt Wine và Lutris

Wine được sử dụng để chạy một số ứng dụng của Windows.

```shell
$ sudo dpkg --add-architecture i386
$ wget -nc https://dl.winehq.org/wine-builds/winehq.key
$ sudo apt-key add winehq.key
$ sudo apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ eoan main'
$ sudo apt update && sudo apt install --install-recommends winehq-stable
```

Trước khi cài đặt Lutris, mình sẽ cài thêm Drive nvidia vì máy mình sử dụng card này.

```shell
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo dpkg --add-architecture i386
$ sudo apt update
$ sudo apt install nvidia-driver-430 libnvidia-gl-430 libnvidia-gl-430:i386
$ sudo apt install libvulkan1 libvulkan1:i386
```

Lutris được sử dụng để cài một số game trong Ubuntu sử dụng Wine.

```shell
$ sudo add-apt-repository ppa:lutris-team/lutris
$ sudo apt-get update
$ sudo apt-get install lutris
```

### 2.7. Cài ibus để gõ tiếng việt

Ibus-bamboo

```shell
$ sudo add-apt-repository ppa:bamboo-engine/ibus-bamboo
$ sudo apt-get update
$ sudo apt-get install ibus-bamboo
$ ibus restart
```

Ibus-Unikey

```shell
$ sudo apt-get install ibus-unikey
```

### 2.8. Cài Font của Microsoft

```shell
$ sudo apt update
$ sudo apt install ttf-mscorefonts-installer -> tab ok -> yes
$ mkdir .fonts
$ wget -qO- http://plasmasturm.org/code/vistafonts-installer/vistafonts-installer | bash
$ sudo fc-cache -f -v
```

### 2.9. Tùy chỉnh Minimize on Click

Cài `dconf-editor` từ Synaptic. Sau đó bật lên chỉnh sửa theo thứ tự sau:

`org/gnome/shell/extensions/dash-to-dock/click-action/`

Các bạn tùy chỉnh:

- Use default value: OFF
- Custom value: minimize

### 2.10. Tùy chỉnh Swap

Mở Terminal lên và xem giá trị Swap:

```shell
$ cat /proc/sys/vm/swappiness
```

Chỉnh sửa bằng cách:

```shell
gedit admin:///etc/sysctl.conf
```

Và thêm dòng sau vào cuối file, lưu và khởi động lại Ubuntu.

```
vm.swappiness = 'gia_tri_sua_lai'
```

### 2.11. Cài đặt tường lửa

Các bạn bật Synaptic lên và tìm ứng dụng sau: `gufw`

### 2.12. Cài đặt thêm một số extension

Nếu các bạn không thích giao diện có sẵn của Ubuntu các bạn có thể tùy chỉnh lại dựa vào một số ứng dụng sau:

Cài đặt Gnome Extension

```shell
$ sudo apt install chrome-gnome-shell
```

Cài đặt Tweaks: Sử dụng Ubuntu Software

Sau đó các bạn vào trang: [GNOME Shell extensions](https://extensions.gnome.org/) để cài thêm một số extension như:

- User Themes
- dash to panel
- arc menu

Các bạn muốn thay đổi theme thì vào trang sau: [GNOME look](https://www.gnome-look.org/) để tải theme, icon về và sử dụng Tweaks để thay đổi.

Tạo 2 thư mục sau:

```shell
mkdir ~/.themes
mkdir ~/.icons
```

Themes và shell tải về, giải nén trong thư mục `.themes` còn icon thì được giải nén trong thư mục `.icons`. Mặc định các thư mục này bị ẩn, các bạn phải bật nó lên.

Trong phần tiếp theo, mình tổng hợp lại một số phần mềm cơ bản nên cài cho Ubuntu và một số phần mềm khác như MySQL, Rstudio, Anaconda để làm việc với Data.

## 3. Cài đặt phần mềm

Trước khi cài đặt phần mềm, ta nên update lại nó bằng lệnh:

```shell
$ sudo apt-get update
```

Thêm kho lưu trữ (repository) phần mềm:

```shell
$ sudo add-apt-repository 'link'
```

Download một phần mềm mà không cài đặt nó:

```shell
$ sudo apt-get download <pack_name>
```

Cài đặt một phần mềm:

```shell
$ sudo apt-get install <pack_name>
```

Xóa phần mềm:

```shell
$ sudo apt-get remove <pack_name>
```

Update tất cả các phần mềm:

```shell
$ sudo apt-get upgrade
```

---
