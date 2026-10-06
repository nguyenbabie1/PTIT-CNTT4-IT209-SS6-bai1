# Bài 1: Khảo sát FHS và Phân quyền File/Folder nâng cao

## 1. Mục tiêu

- Tạo và quản lý thư mục theo chuẩn Linux FHS.
- Thực hành phân quyền bằng `chmod`.
- Thay đổi Owner và Group bằng `chown`.
- Kiểm tra quyền truy cập của thư mục bằng `ls -la`.

---

## 2. Yêu cầu bài tập

Tạo thư mục ứng dụng tại:

```bash
/var/www/my-app
```

Bao gồm:

```text
/var/www/my-app/
├── public/
└── logs/
```

Trong đó:

- `public`: Owner có toàn quyền, Group có quyền đọc/truy cập, Others không có quyền.
- `logs`: Owner và Group có toàn quyền, Others không có quyền.
- Owner: `devops`
- Group: `www-data`

---

## 3. Các bước thực hiện

### Bước 1: Tạo cấu trúc thư mục

```bash
sudo mkdir -p /var/www/my-app/public
sudo mkdir -p /var/www/my-app/logs
```

Kiểm tra:

```bash
ls -la /var/www/my-app
```

---

### Bước 2: Phân quyền thư mục public

Thiết lập quyền `750`:

```bash
sudo chmod 750 /var/www/my-app/public
```

Ý nghĩa:

```text
7 = rwx : Owner có quyền đọc, ghi và truy cập
5 = r-x : Group có quyền đọc và truy cập
0 = --- : Others không có quyền
```

Quyền mong đợi:

```text
drwxr-x---
```

---

### Bước 3: Phân quyền thư mục logs

Thiết lập quyền `770`:

```bash
sudo chmod 770 /var/www/my-app/logs
```

Ý nghĩa:

```text
7 = rwx : Owner có toàn quyền
7 = rwx : Group có toàn quyền
0 = --- : Others không có quyền
```

Quyền mong đợi:

```text
drwxrwx---
```

---

### Bước 4: Đổi Owner và Group

Gán user thường `devops` làm Owner và group `www-data` làm Group:

```bash
sudo chown -R devops:www-data /var/www/my-app
```

Kiểm tra lại:

```bash
ls -la /var/www/my-app
```

---

## 4. Các lệnh thực hiện đầy đủ

```bash
sudo mkdir -p /var/www/my-app/public
sudo mkdir -p /var/www/my-app/logs

sudo chmod 750 /var/www/my-app/public
sudo chmod 770 /var/www/my-app/logs

sudo chown -R devops:www-data /var/www/my-app

ls -la /var/www/my-app
```

---

## 5. Kết quả kiểm tra

Lệnh:

```bash
ls -la /var/www/my-app
```

Kết quả mong đợi tương tự:

```text
total 8
drwxr-xr-x 4 devops www-data 4096 Oct  6 20:30 .
drwxr-xr-x 3 root   root     4096 Oct  6 20:30 ..
drwxrwx--- 2 devops www-data 4096 Oct  6 20:30 logs
drwxr-x--- 2 devops www-data 4096 Oct  6 20:30 public
```

Trong đó:

| Thư mục | Permission | Owner | Group |
|---|---|---|---|
| `public` | `drwxr-x---` (`750`) | `devops` | `www-data` |
| `logs` | `drwxrwx---` (`770`) | `devops` | `www-data` |

---

## 6. Kiểm tra chi tiết quyền

Có thể kiểm tra riêng từng thư mục:

```bash
ls -ld /var/www/my-app/public
ls -ld /var/www/my-app/logs
```

Kết quả mong đợi:

```text
drwxr-x--- 2 devops www-data ... /var/www/my-app/public
drwxrwx--- 2 devops www-data ... /var/www/my-app/logs
```

---

## 7. Giải thích ngắn gọn

### FHS

Thư mục `/var` thường chứa dữ liệu thay đổi trong quá trình hệ thống hoạt động.

Thư mục `/var/www` thường được sử dụng để lưu dữ liệu và mã nguồn phục vụ Web Server.

### chmod

`chmod` dùng để thay đổi quyền của file hoặc thư mục.

Ví dụ:

```bash
chmod 750 public
```

- Owner: `7 = rwx`
- Group: `5 = r-x`
- Others: `0 = ---`

### chown

`chown` dùng để thay đổi Owner và Group.

Ví dụ:

```bash
sudo chown -R devops:www-data /var/www/my-app
```

Trong đó:

- `devops`: Owner.
- `www-data`: Group.
- `-R`: áp dụng cho toàn bộ thư mục con.

---

## 8. Kết luận

Đã hoàn thành:

- Tạo `/var/www/my-app/public`.
- Tạo `/var/www/my-app/logs`.
- Phân quyền `public` là `750`.
- Phân quyền `logs` là `770`.
- Gán Owner là `devops`.
- Gán Group là `www-data`.
- Kiểm tra thành công bằng `ls -la /var/www/my-app`.

---

## 9. Đường dẫn nộp bài

```text
homework/session_06/ex1/README.md
```
