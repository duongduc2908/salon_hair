# Long Hair Salon – Hướng dẫn website & trang quản trị

## Cấu trúc thư mục

| Thư mục / file | Nội dung |
|---|---|
| `index.html` | Giao diện website (bố cục, màu sắc, chữ cố định) |
| `content/salon.json` | Thông tin tiệm: địa chỉ, hotline, giờ mở cửa, link, ảnh đầu trang |
| `content/services.json` | Bảng giá dịch vụ |
| `content/gallery.json` | Ảnh tác phẩm, ảnh trước/sau, vòng tròn kiểu story |
| `content/extras.json` | Dòng chữ chạy, cam kết, đánh giá, câu hỏi thường gặp |
| `photos/` | Ảnh của web. Ảnh tải lên qua trang quản trị nằm trong `photos/uploads/` |
| `photos/fb/` | 111 ảnh gốc lấy từ Facebook (không dùng trực tiếp trên web) |
| `admin/index.html` | Portal quản trị riêng của Long Hair |
| `admin/decap/` | Trang quản trị dự phòng (Decap CMS), dùng khi portal gặp lỗi |

Bình thường bạn **không cần sửa file nào**. Mọi nội dung đều sửa được ở trang `/admin`.

---

## Đưa web lên mạng (làm một lần)

Cần 2 tài khoản miễn phí: **GitHub** (lưu code) và **Netlify** (chạy web).

### Bước 1. Đưa code lên GitHub
1. Tạo tài khoản ở https://github.com.
2. Tạo repository mới tên `long-hair-salon` (Private cũng được).
3. Cài **GitHub Desktop** (https://desktop.github.com), chọn *Add existing repository* → thư mục `salon_hair` → *Publish repository*.
   (Nếu dùng dòng lệnh: `git init`, `git add .`, `git commit -m "Website Long Hair Salon"`, rồi `git remote add origin …` và `git push -u origin main`.)

### Bước 2. Cấu hình repo cho trang quản trị (đã làm sẵn)
Tên repo và địa chỉ web nằm ở 2 chỗ, đã điền sẵn `duongduc2908/salon_hair` và `https://profound-unicorn-9725a5.netlify.app`:
- `admin/index.html`, phần `CONFIG` ở đầu đoạn script (portal chính)
- `admin/decap/config.yml` (trang dự phòng)

Nếu sau này đổi tên web Netlify hoặc chuyển repo, sửa cả 2 chỗ này.

### Bước 3. Tạo web trên Netlify
1. Đăng nhập https://app.netlify.com bằng tài khoản GitHub.
2. *Add new site* → *Import an existing project* → *GitHub* → chọn `long-hair-salon`.
3. Để trống *Build command*, *Publish directory* điền `.` → *Deploy*.
4. Sau khoảng 1 phút web chạy ở địa chỉ dạng `https://xxx.netlify.app`. Có thể đổi tên trong *Site configuration → Change site name*, hoặc gắn tên miền riêng (VD: longhairsalon.vn) ở *Domain management*.

### Bước 4. Cho phép đăng nhập admin bằng GitHub
1. Trên GitHub: ảnh đại diện → *Settings* → *Developer settings* → *OAuth Apps* → *New OAuth App*:
   - **Application name:** Long Hair Salon Admin
   - **Homepage URL:** địa chỉ web Netlify của bạn
   - **Authorization callback URL:** `https://api.netlify.com/auth/done`
2. Bấm *Register*, chép **Client ID**, bấm *Generate a new client secret* và chép **Client secret**.
3. Trên Netlify: *Site configuration* → *Access & security* → *OAuth* → *Install provider* → **GitHub** → dán Client ID và Client secret → *Install*.

### Bước 5. Vào trang quản trị
Mở `https://ten-web-cua-ban.netlify.app/admin/` → **Đăng nhập bằng GitHub**.

**Thêm người cùng quản lý:** trên GitHub vào repo → *Settings* → *Collaborators* → *Add people*. Người đó cần có tài khoản GitHub.

---

## Dùng trang quản trị hằng ngày

Địa chỉ: **https://profound-unicorn-9725a5.netlify.app/admin/** → **Đăng nhập bằng GitHub**.

| Mục | Làm được gì |
|---|---|
| **Tổng quan** | Số dịch vụ, số ảnh, lối tắt tới việc hay làm, lịch sử các lần lưu |
| **Bảng giá** | Sửa giá ngay trên dòng; bấm ✏️ để sửa tên, thời gian, mô tả (VI + EN); ↑ ↓ đổi thứ tự; 🗑 xóa; thêm dịch vụ, thêm nhóm |
| **Ảnh** | 3 thẻ: Tác phẩm, Trước & sau, Vòng tròn đầu trang. Bấm “Đổi ảnh” hoặc “Thêm ảnh”, ảnh được tự thu nhỏ trước khi tải lên |
| **Thông tin tiệm** | Tên, slogan, địa chỉ, hotline, giờ mở cửa, link Facebook/Messenger/Zalo/Maps, số liệu, ảnh chính |
| **Cam kết & đánh giá** | Dòng chữ chạy (khuyến mãi), cam kết, đánh giá của khách, câu hỏi thường gặp |

Sửa xong bấm **Lưu & công bố** ở góc trên bên phải. Khoảng 1 phút sau website cập nhật.
Chấm vàng cạnh tên mục ở menu trái = mục đó có thay đổi chưa lưu. **Hoàn tác** bỏ mọi thay đổi chưa lưu.

**Mẹo:**
- **Giá** nhập theo nghìn đồng: `699` hiển thị là `699K`. Để trống ô giá thì web hiện "Báo giá". Tick **“từ”** để hiện “từ 699K”.
- **Ảnh**: ảnh vuông cho lưới tác phẩm và trước/sau, ảnh dọc 4:5 cho ảnh đầu trang. Ảnh tải lên nằm trong `photos/uploads/`.
- **Lưới tác phẩm**: để số ảnh chia hết cho 3 (6, 9, 12…) cho lưới đều.
- **Lịch sử**: mỗi lần lưu là một commit trên GitHub, có thể khôi phục bản cũ nếu sửa nhầm.
- **Dự phòng**: nếu portal gặp lỗi, vẫn sửa được ở `/admin/decap/` (Decap CMS, cùng nội dung).

Những chữ cố định của giao diện (tiêu đề các phần, nhãn nút) nằm trong `index.html`, phần `STR` ở cuối file.

---

## Sửa thử trên máy tính (không cần mạng)

Trong thư mục `salon_hair`, mở 2 cửa sổ Terminal:
```bash
npx decap-server            # cửa sổ 1
python3 -m http.server 8000 # cửa sổ 2
```
Mở http://localhost:8000/admin/ → **Vào chế độ máy tính** (không cần mật khẩu). Thay đổi được ghi thẳng vào các file trong `content/`. Xem web ở http://localhost:8000.

Lưu ý: không mở trực tiếp file `index.html` bằng cách nhấp đúp, vì trình duyệt sẽ chặn việc đọc file `content/*.json`. Luôn mở qua `http://localhost:8000`.
