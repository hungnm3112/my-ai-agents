## QUY CHUẨN BỐ CỤC TÀI LIỆU API & COLLECTION KIỂM THỬ

### 1. Bố cục 4 Phần của File Tài liệu API (`md/analysis/6-api-specification.md` hoặc `md/analysis/api-module-xx.md`)
0. **Phần 0 — Kịch bản Luồng gọi API theo Màn hình (FE-First Sequence Scenarios):** Sơ đồ `sequenceDiagram` mô tả trình tự gọi API giữa Frontend, Backend và Hệ thống tích hợp theo thao tác thực tế của người dùng.
1. **Mục 1 — Quy ước chung & Ma trận Phân quyền (RBAC):** Quy ước Header xác thực (ví dụ `req.headers.token` / `req.cookies.token`), bảng quyền của từng Role và danh mục mã quyền thực tế trong DB (`function_id` hoặc `<resource>.<action>`).
2. **Mục 2 — Bảng Danh sách Tổng hợp API:** Cột `# | Method | Endpoint | Chức năng (Mã FDD) | Quyền`.
3. **Mục 3 — Chi tiết từng API:**
   - `Method` + `Endpoint` + `Quyền truy cập`.
   - `Query Parameters` (`snake_case`, định dạng ngày chuẩn ISO 8601 `YYYY-MM-DD`) hoặc `Request Body` JSON mẫu (`snake_case`).
   - Bảng điều kiện Validate (`Trường | Bắt buộc | Kiểm tra`).
   - Logic xử lý ngầm tại Service.
   - `Response 200 / 201 / 202` JSON mẫu và các mã lỗi có thể xảy ra.
4. **Mục 4 — Bảng Tổng hợp Điều kiện Chặn xóa & Lỗi Nghiệp vụ (`403 / 409`):** Ghi rõ chính sách xóa dữ liệu và bảng mã lỗi toàn hệ thống.

### 2. Chuẩn Collection Postman / Thunder Client
- Chia folder theo đúng cấu trúc nhánh FDD; đặt tên request gắn kèm mã FDD.
- Không hardcode URL, Token hay ID; bắt buộc dùng biến môi trường đồng bộ với tên biến trong code thực tế: `{{base_url}}`, `{{token}}` *(hoặc `{{access_token}}` tùy cơ chế Auth của dự án)*, `{{..._id}}`.
- Cấu hình Authorization ở cấp Root Collection (ví dụ `API Key` với `Key: token`, `Value: {{token}}`, `Add to: Header`) và để các Request con kế thừa (`Inherit auth from parent`).

