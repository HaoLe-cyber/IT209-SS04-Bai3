# Báo cáo Bài 3: Cấu hình xác thực SSH và Đẩy dự án lên GitHub

## 1. Sinh cặp khóa SSH với thuật toán Ed25519
Mở terminal (hoặc Git Bash) và chạy lệnh sau để khởi tạo cặp khóa SSH sử dụng thuật toán Ed25519:

```bash
ssh-keygen -t ed25519 -C "youremail@example.com"
```
*(Lưu ý: Thay `youremail@example.com` bằng email đăng ký tài khoản GitHub của bạn. Nhấn `Enter` để chấp nhận đường dẫn lưu mặc định và nhập/bỏ qua passphrase).*

Đọc và sao chép nội dung khóa public vừa tạo:
```bash
cat ~/.ssh/id_ed25519.pub
```

Sau đó, truy cập GitHub -> **Settings** -> **SSH and GPG keys** -> **New SSH key**, dán khóa công khai (public key) vào và nhấn **Add SSH key**.

---

## 2. Kiểm tra kết nối SSH tới GitHub
Chạy lệnh sau để kiểm tra xác thực SSH với máy chủ GitHub:

```bash
ssh -T git@github.com
```

**Kết quả mong đợi:**
```text
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 3. Cấu hình Remote URL và đẩy dự án lên GitHub

### 3.1. Cấu hình đường dẫn Remote dạng SSH
Chuyển sang thư mục dự án cục bộ (local repository) và thực hiện liên kết tới GitHub qua SSH:

```bash
# Nếu chưa có remote origin:
git remote add origin git@github.com:username/repository.git

# Hoặc nếu đã có remote origin (HTTPS) và muốn chuyển sang SSH:
git remote set-url origin git@github.com:username/repository.git
```
*(Thay `username/repository.git` bằng tên tài khoản và tên kho lưu trữ của bạn trên GitHub).*

### 3.2. Kiểm tra lại cấu hình remote URL
```bash
git remote -v
```

**Kết quả mong đợi:**
```text
origin  git@github.com:username/repository.git (fetch)
origin  git@github.com:username/repository.git (push)
```

### 3.3. Đẩy (Push) mã nguồn lên GitHub
```bash
git push -u origin main
```

---

## 4. Thông tin Repository
- **Đường dẫn Repository (GitHub URL):** `https://github.com/username/repository`
- **Đường dẫn SSH:** `git@github.com:username/repository.git`