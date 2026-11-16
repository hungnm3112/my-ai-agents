## QUY TẮC ĐẶT TÊN TOÀN DỰ ÁN (NAMING CONVENTIONS)

| Thành phần | Quy ước | Ví dụ chuẩn |
|---|---|---|
| **Thư mục (Folder Module)** | `snake_case` | `src/models/daily_report_timekeeper/`, `public/js/daily_report_timekeeper/` |
| **Tên File (Backend, View, JS)** | `snake_case` | `daily_checklist.js`, `daily_report_timekeeper_service.js`, `desktop.ejs`, `model.js` |
| **Biến & Hàm (JS/TS)** | `snake_case` | `const employee_id = ...;`, `function get_daily_reports() {}` |
| **Class & Interface / Type** | `PascalCase` | `class DailyReportTimekeeperService {}`, `class DailyReportTimekeeperController {}` |
| **Hằng số & Biến môi trường** | `UPPER_SNAKE_CASE` | `const MAX_RETRY_COUNT = 3;`, `FUNCTION_VIEW_REPORT_ID` |
| **Database Collection (Bảng)** | `PascalCase` (tường minh) | `{ collection: 'DailyChecklist' }`, `'Employee'`, `'Branch'` |
| **Database Fields (Trường)** | `snake_case` | `employee_id`, `branch_id`, `total_amount` *(Ngoại lệ: `_id`, `ID`, `createdAt`, `updatedAt`)* |
| **API Endpoint & URL Route** | Danh từ số nhiều, `kebab-case` | `/daily-report-timekeeper`, `/api/v1/daily-checklists` |
| **API Body & Response** | `snake_case` (trùng DB) | `{ "employee_id": "...", "tasks": [], "total_pages": 5 }` |
| **API Query Parameters** | `snake_case` (đồng bộ DB) | `?page=1&limit=20&branch_id=...&from_date=YYYY-MM-DD&to_date=YYYY-MM-DD` |
