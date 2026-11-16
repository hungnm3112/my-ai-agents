## QUY TẮC MONGOOSE SCHEMA & TỐI ƯU TRUY VẤN

### 1. Khai báo Mongoose Schema
- Đặt trong thư mục `models/<module_name>/` (hoặc `schemas/` của từng module).
- Bắt buộc cấu hình tên Collection tường minh theo chuẩn **`PascalCase`**: `{ collection: 'YourCollectionName', timestamps: true }` (ví dụ: `{ collection: 'DailyChecklist', timestamps: true }`) và khai báo rõ `type`, `required`, `default`, `index`.

### 2. Tối ưu Truy vấn (Read, Update & Aggregation)
- **Read:** Luôn dùng `.select(...)` chỉ lấy các trường cần thiết và `.lean()` cho truy vấn chỉ đọc.
- **Validate ObjectId:** Luôn kiểm tra `Types.ObjectId.isValid(id)` trước khi query DB (sai trả `400 Bad Request`).
- **Update:** Ưu tiên `findOneAndUpdate()`, `updateOne()`, `updateMany()`, `bulkWrite()`; tránh dùng `.save()` trong vòng lặp.
- **Aggregation Pipeline:**
  - Thứ tự chuẩn: `$match` (sớm nhất) ➔ `$lookup` ➔ `$unwind` ➔ `$group` ➔ `$project` ➔ `$sort` ➔ `$skip` ➔ `$limit`.
  - Bật `.allowDiskUse(true)`, xử lý rỗng bằng `$ifNull` và chống `NaN` bằng `$cond` + `$isNumber`.

