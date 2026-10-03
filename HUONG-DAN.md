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
| `admin/` | Trang quản trị (Decap CMS) |

Bình thường bạn **không cần sửa file nào**. Mọi nội dung đều sửa được ở trang `/admin`.

---

## Đưa web lên mạng (làm một lần)

Cần 2 tài khoản miễn phí: **GitHub** (lưu code) và **Netlify** (chạy web).

### Bước 1. Đưa code lên GitHub
1. Tạo tài khoản ở https://github.com.
2. Tạo repository mới tên `long-hair-salon` (Private cũng được).
3. Cài **GitHub Desktop** (https://desktop.github.com), chọn *Add existing repository* → thư mục `salon_hair` → *Publish repository*.
   (Nếu dùng dòng lệnh: `git init`, `git add .`, `git commit -m "Website Long Hair Salon"`, rồi `git remote add origin …` và `git push -u origin main`.)

### Bước 2. Sửa tên repo trong cấu hình admin
Mở `admin/config.yml`, sửa 2 chỗ có dấu ←:
```yaml
repo: TEN-GITHUB-CUA-BAN/long-hair-salon
site_url: https://ten-web-cua-ban.netlify.app
```
Lưu lại rồi đẩy lên GitHub (GitHub Desktop: *Commit* → *Push*).

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

1. Vào `/admin/` và đăng nhập.
2. Chọn mục ở cột trái: **Thông tin tiệm**, **Bảng giá**, **Ảnh**, **Cam kết, đánh giá, FAQ**.
3. Sửa nội dung. Mỗi mục có ô **tiếng Việt** và ô **tiếng Anh** riêng.
4. Bấm **Công bố** (Publish) ở góc trên. Khoảng 1 phút sau web tự cập nhật.

**Mẹo:**
- **Giá** nhập theo nghìn đồng: `699` hiển thị là `699K`. Để trống ô giá thì web hiện "Báo giá".
- **Thứ tự**: kéo biểu tượng ═ để đổi thứ tự dịch vụ, ảnh, câu hỏi.
- **Ảnh**: nên dùng ảnh vuông cho lưới tác phẩm và ảnh trước/sau, ảnh dọc 4:5 cho ảnh đầu trang. Ảnh dưới 500 KB giúp web tải nhanh.
- **Lưới tác phẩm**: để số ảnh chia hết cho 3 (6, 9, 12…) cho lưới đều.
- **Vòng tròn đầu trang**: ô "Bấm vào thì đi tới" điền mã nhóm dịch vụ (`cut`, `perm`, `colour`, `care`) để mở bảng giá nhóm đó, hoặc `#before-after`, `#grid`, `#space`, `#visit` để nhảy tới phần tương ứng.
- **Lịch sử**: mọi thay đổi được lưu trên GitHub, có thể khôi phục bản cũ nếu sửa nhầm.

Những chữ cố định của giao diện (tiêu đề các phần, nhãn nút) nằm trong `index.html`, phần `STR` ở cuối file.

---

## Sửa thử trên máy tính (không cần mạng)

Trong thư mục `salon_hair`, mở 2 cửa sổ Terminal:
```bash
npx decap-server            # cửa sổ 1
python3 -m http.server 8000 # cửa sổ 2
```
Mở http://localhost:8000/admin/ → *Đăng nhập* (không cần mật khẩu khi chạy trên máy). Thay đổi được ghi thẳng vào các file trong `content/`. Xem web ở http://localhost:8000.

Lưu ý: không mở trực tiếp file `index.html` bằng cách nhấp đúp, vì trình duyệt sẽ chặn việc đọc file `content/*.json`. Luôn mở qua `http://localhost:8000`.
