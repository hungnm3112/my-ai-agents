## AGENT BEHAVIOR: CLARIFY & SUGGEST BEFORE MAJOR CODE CHANGES

### 1. Scope & Triggers (Khi nào áp dụng?)
Bắt buộc kích hoạt quy trình "Chẩn đoán & Đưa phương án" đối với:
- Thay đổi logic lớn, tái cấu trúc (refactoring) ảnh hưởng từ 2 file/module trở lên.
- Thay đổi Database Schema, luồng nghiệp vụ hoặc API contracts.
- Bài toán/lỗi có nhiều hướng giải quyết với các trade-off kỹ thuật khác nhau.

### 2. Exceptions (Khi nào BỎ QUA để thực hiện/sửa code ngay?)
Bỏ qua bước hỏi phương án và **thực thi sửa trực tiếp** nếu:
- **Trivial / Direct Fixes**: Lỗi hiển nhiên (typo, cú pháp, thiếu import, null/undefined check, sửa style nhỏ).
- **Single Obvious Solution**: Bugfix đã xác định rõ dòng lỗi qua stacktrace và chỉ có duy nhất một cách sửa chuẩn.
- **Explicit Instruction**: Người dùng ra lệnh trực tiếp thực thi (ví dụ: *"fix ngay lỗi này"*, *"sửa luôn theo cách X"*).

---

### 3. Workflow for Major Changes (Quy trình khi áp dụng)
Khi gặp vấn đề thuộc diện áp dụng, **KHÔNG** tự ý sửa code ngay. Thực hiện đúng 3 bước:

1. **Problem Diagnosis**: 
   - Giải thích ngắn gọn (1-2 câu) về nguyên nhân gốc rễ hoặc thách thức kiến trúc.
2. **Contextual Options (2-3 phương án)**:
   - **Option A (Recommended)**: Tên hướng tiếp cận - Tóm tắt cách làm + Ưu/Nhược điểm (trade-offs) + Lý do khuyến nghị.
   - **Option B**: Hướng tiếp cận thay thế + Ưu/Nhược điểm.
   - **Option C (Tùy chọn)**: Giải pháp tạm thời (quick fix) hoặc tái cấu trúc triệt để (radical refactor).
3. **Awaiting Decision**:
   - Dừng lại và hỏi người dùng muốn chọn Option nào hoặc muốn điều chỉnh hướng đi trước khi viết code.