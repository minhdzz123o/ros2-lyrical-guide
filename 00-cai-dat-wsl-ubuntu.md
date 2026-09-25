# 🖥️ Hướng Dẫn Cài Đặt WSL & Ubuntu Trên Windows

> Đây là bước **tiên quyết** trước khi cài ROS 2. Nếu bạn dùng Windows, bạn cần cài WSL + Ubuntu để có môi trường Linux chạy ROS 2.

---

## WSL là gì? Tại sao cần nó?

**WSL (Windows Subsystem for Linux)** là tính năng của Windows cho phép bạn **chạy hệ điều hành Linux ngay bên trong Windows**, không cần cài dual-boot, không cần máy ảo nặng nề.

### Tại sao phải dùng WSL để học ROS 2?

| | Windows thuần | WSL + Ubuntu |
|:---|:---:|:---:|
| ROS 2 hỗ trợ chính thức | ❌ Rất hạn chế | ✅ Đầy đủ 100% |
| Cài đặt bằng `apt install` | ❌ | ✅ |
| Chạy RViz, Gazebo | ❌ Khó cấu hình | ✅ Chạy trực tiếp |
| Tài liệu và cộng đồng hỗ trợ | ❌ Rất ít | ✅ Đa số tutorial viết cho Linux |

> 💡 **Tóm lại:** ROS 2 được thiết kế chạy trên Linux. WSL giúp bạn có Linux ngay trên Windows mà **không mất dữ liệu**, không ảnh hưởng gì đến Windows đang dùng.

---

## 📋 Yêu cầu hệ thống

- **Windows 10** phiên bản 2004 trở lên (Build 19041+), hoặc **Windows 11** bất kỳ
- RAM tối thiểu **8 GB** (khuyến nghị 16 GB)
- Ổ cứng còn trống tối thiểu **10 GB**

> Để kiểm tra phiên bản Windows: nhấn `Win + R` → gõ `winver` → nhấn Enter.

---

## Bước 1: Bật tính năng WSL trên Windows

### 💻 Cách làm:

1. Mở **PowerShell** với quyền **Administrator**:
   - Nhấn phím `Win`, gõ `PowerShell`
   - Click chuột phải → chọn **"Run as Administrator"**

2. Gõ lệnh sau rồi nhấn **Enter**:

```powershell
wsl --install
```

3. **Đợi** hệ thống tải và cài đặt xong (mất khoảng 2-5 phút tùy mạng)

4. **Khởi động lại máy tính** khi được yêu cầu

### 🔍 Lệnh `wsl --install` làm gì?

Lệnh này tự động thực hiện **3 việc** cùng lúc:
- ✅ Bật tính năng **Windows Subsystem for Linux**
- ✅ Bật tính năng **Virtual Machine Platform**
- ✅ Tải và cài đặt **Ubuntu** (phiên bản mặc định mới nhất)

> ⚠️ **Bắt buộc phải khởi động lại máy!** Nếu không restart, WSL sẽ không hoạt động.

---

## Bước 2: Cài Ubuntu từ Microsoft Store (Chọn phiên bản cụ thể)

> Nếu ở Bước 1 lệnh `wsl --install` đã tự cài Ubuntu mặc định cho bạn rồi, bạn có thể **bỏ qua** bước này. Tuy nhiên nếu bạn muốn cài **đúng phiên bản Ubuntu cụ thể** (ví dụ Ubuntu 26.04 cho ROS 2 Lyrical, hoặc Ubuntu 24.04 cho ROS 2 Jazzy), hãy làm theo hướng dẫn dưới đây.

### 💻 Cách làm:

1. Mở **Microsoft Store** trên Windows (nhấn phím `Win`, gõ `Microsoft Store`)

2. Trong ô tìm kiếm, gõ: **`Ubuntu`**

3. Bạn sẽ thấy nhiều phiên bản. **Chọn đúng phiên bản** phù hợp với ROS 2 bạn muốn cài:

| Phiên bản Ubuntu | ROS 2 tương ứng | Chọn cái nào trên Store |
|:---|:---|:---|
| Ubuntu 26.04 | ROS 2 **Lyrical** | Tìm `Ubuntu 26.04 LTS` |
| Ubuntu 24.04 | ROS 2 **Jazzy** | Tìm `Ubuntu 24.04 LTS` |

4. Bấm nút **"Get"** hoặc **"Install"** → đợi tải xong (khoảng 500 MB - 1 GB)

5. Sau khi cài xong, bấm **"Open"** để mở Ubuntu lần đầu tiên

---

## Bước 3: Thiết lập tài khoản Ubuntu lần đầu

Khi mở Ubuntu lần đầu, hệ thống sẽ yêu cầu bạn tạo tài khoản:

```text
Installing, this may take a few minutes...
Please create a default UNIX user account.
The username should not include uppercase letters.
Enter new UNIX username:
```

### 💻 Thao tác:

1. **Gõ tên người dùng** (viết thường, không dấu, không khoảng trắng):
   ```text
   Enter new UNIX username: huyminhcp
   ```

2. **Gõ mật khẩu** (bạn gõ nhưng màn hình **không hiện ký tự** nào — đây là bình thường, cứ gõ rồi nhấn Enter):
   ```text
   New password: ********
   Retype new password: ********
   ```

3. Khi thấy dòng xanh lá kiểu `huyminhcp@HUYMINHcp:~$` nghĩa là **đã vào Ubuntu thành công!**

> ⚠️ **Nhớ mật khẩu này!** Mỗi lần chạy lệnh `sudo` (quyền quản trị), Ubuntu sẽ hỏi lại mật khẩu này.

---

## Bước 4: Cập nhật Ubuntu ngay sau khi cài

Bước đầu tiên sau khi vào Ubuntu luôn là cập nhật hệ thống:

```bash
sudo apt update && sudo apt upgrade -y
```

Đợi chạy xong (mất 1-3 phút). Từ bây giờ, bạn đã có một **hệ điều hành Ubuntu đầy đủ** chạy ngay trên Windows để cài ROS 2!

---

## 🗂️ Cách truy cập file giữa Windows ↔ Ubuntu

### Từ Ubuntu → truy cập file Windows:

Toàn bộ ổ đĩa Windows được gắn (mount) tại `/mnt/`:

```bash
# Truy cập ổ C:
cd /mnt/c/

# Truy cập thư mục Desktop
cd /mnt/c/Users/TÊN_BẠN/Desktop/

# Truy cập ổ D:
cd /mnt/d/
```

### Từ Windows → truy cập file Ubuntu:

Mở **File Explorer** (cửa sổ quản lý file trên Windows), gõ vào thanh địa chỉ:

```text
\\wsl$
```

Bạn sẽ thấy thư mục Ubuntu hiện ra, có thể kéo thả file qua lại bình thường.

---

## 📌 Các lệnh WSL hữu ích (Chạy trên PowerShell Windows)

| Lệnh | Công dụng |
|:---|:---|
| `wsl` | Mở Ubuntu (WSL mặc định) |
| `wsl --list --verbose` | Xem danh sách các bản Ubuntu đã cài + trạng thái |
| `wsl --set-default Ubuntu-26.04` | Đặt Ubuntu 26.04 làm bản mặc định |
| `wsl --shutdown` | Tắt hoàn toàn WSL (giải phóng RAM) |
| `wsl --update` | Cập nhật WSL lên phiên bản mới nhất |
| `wsl --unregister Ubuntu-26.04` | **Xóa sạch** bản Ubuntu (⚠️ mất hết dữ liệu!) |

---

## 🔧 Các cách mở Ubuntu hàng ngày

Sau khi cài xong, bạn có **3 cách** mở Ubuntu:

| Cách | Thao tác |
|:---|:---|
| **Cách 1** | Nhấn phím `Win` → gõ `Ubuntu` → click vào biểu tượng Ubuntu |
| **Cách 2** | Mở **Windows Terminal** → bấm mũi tên ▼ cạnh tab → chọn `Ubuntu` |
| **Cách 3** | Mở **PowerShell** hoặc **CMD** → gõ `wsl` rồi nhấn Enter |

> 💡 **Khuyên dùng Cách 2** — Windows Terminal cho phép mở nhiều tab Ubuntu cùng lúc, rất tiện khi làm việc với ROS 2 (cần 2 terminal chạy Talker & Listener, v.v.)

---

## ❓ Lỗi thường gặp khi cài WSL

| Lỗi | Nguyên nhân | Cách sửa |
|:---|:---|:---|
| `WslRegisterDistribution failed with error: 0x80370102` | Chưa bật Virtualization trong BIOS | Vào BIOS → bật **Intel VT-x** hoặc **AMD-V** |
| `wsl --install` không chạy | PowerShell không có quyền Admin | Click chuột phải → **Run as Administrator** |
| `The WSL 2 kernel file is not found` | WSL chưa được cập nhật | Chạy `wsl --update` trên PowerShell |
| Ubuntu mở lên rồi tắt ngay | WSL chưa restart sau cài đặt | **Khởi động lại máy tính** |
| Gõ mật khẩu nhưng không thấy gì trên màn hình | Đây là **đặc điểm bảo mật** của Linux | Cứ gõ mật khẩu bình thường rồi nhấn Enter, Linux cố ý không hiện ký tự |

---

## ✅ Sau khi cài xong WSL + Ubuntu

Bạn đã sẵn sàng chuyển sang bước tiếp theo:

👉 **[Cài đặt ROS 2 Lyrical trên Ubuntu](./ros2-lyrical-install-guide.md)**
