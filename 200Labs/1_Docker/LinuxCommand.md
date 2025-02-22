# Hướng dẫn quản lý người dùng và SSH trong Linux

## 1. Phân quyền truy cập tập tin (File Permissions)

### a) Các quyền cơ bản

Trong Linux, mỗi tệp và thư mục có 3 loại quyền:

- **r (read - đọc)**: Xem nội dung tệp/thư mục.
- **w (write - ghi)**: Chỉnh sửa hoặc xóa tệp/thư mục.
- **x (execute - thực thi)**: Chạy tệp dưới dạng chương trình.

Ba nhóm người dùng có thể sở hữu quyền trên:

- **Owner (chủ sở hữu)**
- **Group (nhóm)**
- **Others (tất cả người khác)**

### b) Kiểm tra quyền tệp

Dùng lệnh sau để xem quyền của tệp/thư mục:

```bash
ls -l
```

Ví dụ:

```bash
-rw-r--r--  1 user group 1234 Feb 22 12:00 myfile.txt
```

- `-rw-r--r--`: Cho biết quyền trên tệp.
- **Owner (`rw-`)**: Có quyền đọc và ghi.
- **Group (`r--`)**: Chỉ có quyền đọc.
- **Others (`r--`)**: Chỉ có quyền đọc.

### c) Thay đổi quyền tệp

Sử dụng lệnh `chmod`:

```bash
chmod u+x myscript.sh  # Cho phép Owner chạy file
chmod g+w myfile.txt   # Cho phép Group ghi file
chmod o-r myfile.txt   # Ngăn Others đọc file
```

Hoặc dùng kiểu số (`chmod 755`):

```bash
chmod 755 myscript.sh  # Owner: rwx, Group: r-x, Others: r-x
```

### d) Thay đổi chủ sở hữu

Dùng `chown` để đổi Owner và Group:

```bash
chown user myfile.txt       # Đổi chủ sở hữu
chown user:group myfile.txt # Đổi chủ sở hữu và nhóm
```

---

## 2. Tạo User và phân quyền

### a) Tạo user mới

```bash
sudo adduser newuser
```

Sau đó đặt mật khẩu cho user.

### b) Thêm user vào nhóm

```bash
sudo usermod -aG groupname newuser
```

### c) Cấp quyền sudo cho user

Nếu muốn user có quyền admin:

```bash
sudo usermod -aG sudo newuser
```

### d) Kiểm tra user

Xem danh sách user trong hệ thống:

```bash
cat /etc/passwd
```

Xem nhóm mà user thuộc về:

```bash
groups newuser
```

---

## 3. Thiết lập SSH để truy cập vào Remote Server

### a) Cài đặt OpenSSH

Trên server:

```bash
sudo apt update && sudo apt install openssh-server -y
```

Kiểm tra trạng thái SSH:

```bash
sudo systemctl status ssh
```

### b) Tạo SSH Key trên máy cá nhân

Trên máy local:

```bash
ssh-keygen -t rsa -b 4096
```

Nó sẽ tạo ra cặp khóa:

- `~/.ssh/id_rsa` (Private key)
- `~/.ssh/id_rsa.pub` (Public key)

### c) Copy Public Key lên Server

Dùng lệnh sau để gửi khóa lên server:

```bash
ssh-copy-id newuser@your-server-ip
```

Hoặc tự thêm vào:

```bash
cat ~/.ssh/id_rsa.pub | ssh newuser@your-server-ip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

### d) Truy cập Server qua SSH

```bash
ssh newuser@your-server-ip
```

Bạn có thể tắt đăng nhập bằng mật khẩu để tăng bảo mật:

```bash
sudo nano /etc/ssh/sshd_config
```

Tìm dòng:

```bash
PasswordAuthentication yes
```

Sửa thành:

```bash
PasswordAuthentication no
```

Sau đó khởi động lại SSH:

```bash
sudo systemctl restart ssh
```
