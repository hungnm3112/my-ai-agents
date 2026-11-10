## QUY TẮC RESTFUL URI, HTTP METHODS & SUB-RESOURCES

### 1. Quy ước Định danh URI & Thứ tự Route
- **Prefix bắt buộc:** `/api/v1/<resources>`.
- **Resource Naming:** Đặt theo **danh từ số nhiều**, chữ thường `kebab-case` của **Tài nguyên Nghiệp vụ (Domain Resource / Virtual Resource)** thay vì phụ thuộc cứng vào tên bảng vật lý trong DB:
  - **CRUD 1 bảng đơn giản:** Đặt theo tên thực thể nghiệp vụ tương ứng (dấu `_` đổi thành `-`, ví dụ: `/api/v1/daily-checklists`).
  - **Truy vấn nhiều bảng / nhiều DB phục vụ 1 phân hệ chính:** Đặt theo `<primary-domain-resources>/<sub-resources>` (ví dụ: `/api/v1/daily-checklists/permissions`, `/api/v1/daily-checklists/statistics`).
  - **Tổng hợp liên phân hệ (Composite / Virtual Resource):** Đặt theo danh từ của khái niệm tổng hợp (ví dụ: `/api/v1/dashboards/overview`, `/api/v1/attendance-reports`).
  - **CẤM** đưa động từ vào URI.
- **Thứ tự Route trong Controller:** Các route tĩnh/đặc thù (`GET /tree`, `GET /lookup`, `GET /trending`, `GET /statistics`, `GET /permissions`) **bắt buộc khai báo phía trên** route động `GET /:id`.

### 2. Quy ước HTTP Methods & Tính Idempotency
- **`GET` (Safe, Idempotent):** Truy vấn danh sách, chi tiết `/:id`, cây `/tree`, tra cứu `/lookup`.
- **`POST` (Non-idempotent):** Tạo mới bản ghi (`201 Created`), kích hoạt tiến trình chạy ngầm (`202 Accepted`), hoặc xác thực phiên (`/auth/login`, `/auth/refresh-token`, `/auth/logout` — `200 OK`).
- **`PUT` (Idempotent) — CẤM DÙNG `PATCH`:** Bắt buộc dùng `PUT` cho **toàn bộ** thao tác cập nhật (cả toàn phần lẫn một phần qua DTO `PartialType`) để tránh lỗi tương thích trên Reverse Proxy/WAF/Cloudflare.
- **`DELETE` (Idempotent):** Xóa cứng bản ghi chưa có tham chiếu (`200 OK`); chặn `409 CONFLICT` nếu đang được tham chiếu.

### 3. Quy tắc Tách Sub-resource khi Cập nhật (`PUT`)
- `PUT /:id`: Chỉ cập nhật thông tin thuộc tính thông thường của bản ghi.
- Các thao tác có **hiệu ứng phụ (side-effects)** hoặc phân quyền riêng phải tách thành sub-resource: `PUT /:id/status`, `PUT /:id/role`, `PUT /:id/password`, `PUT /auth/password`.

