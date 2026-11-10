## QUY TẮC REQUEST BODY & QUERY PARAMETERS

### 1. Request Body (`POST` / `PUT`)
- Toàn bộ tên trường trong JSON Request Body bắt buộc dùng **`snake_case`**, trùng khớp 100% với tên trường trong Database (`role_id`, `parent_id`, `warehouse_ids`).
- Client không bao giờ gửi các trường tự sinh nội bộ của Server (`_id`, `unsign_search`, `createdAt`, `updatedAt`).

### 2. Query String Parameters (`GET`)
- Toàn bộ tham số điều khiển trên URL Query String bắt buộc dùng **`snake_case`** (đồng bộ 100% với tên trường trong Database và JSON Body).
- Mọi API lấy danh sách (`GET /api/v1/resources`) **bắt buộc hỗ trợ bộ tham số chuẩn**:
  `?page=1&limit=20&keyword=...&status=1&from_date=YYYY-MM-DD&to_date=YYYY-MM-DD`
- Định dạng ngày tháng truyền qua Query Parameters (`date`, `from_date`, `to_date`...) bắt buộc thống nhất theo chuẩn quốc tế **ISO 8601 (`YYYY-MM-DD`, ví dụ: `2026-11-10`)** để tránh lỗi parse ngày/tháng.
- Các tham số lọc theo khóa ngoại hoặc thuộc tính riêng cũng viết theo `snake_case`: `role_id`, `branch_id`, `employee_id`, `category_id`, `parent_id`, `warehouse_id`, `type`, `sort_by`.
