## QUY TẮC VÒNG LẶP HỎI - ĐÁP TRONG PHÂN TÍCH & THIẾT KẾ (ITERATIVE Q&A & CLARIFICATION LOOP)

### 1. Phạm vi Áp dụng Bắt buộc
Quy tắc này áp dụng xuyên suốt tất cả các bước trong chuỗi phân tích & thiết kế (`Bước 1` đến `Bước 6` trong `workflow_phases.md`) và các bài toán kiến trúc/logic lớn có nhiều phương án giải quyết.

### 2. Quy trình Chu trình Hỏi - Đáp Bắt buộc (4 Giai đoạn)

**TUYỆT ĐỐI KHÔNG** tự ý suy diễn câu trả lời và **KHÔNG** tạo/ghi file tài liệu `.md` hay viết code trước khi hoàn thành trọn vẹn 4 giai đoạn sau:

#### Giai đoạn 1: Đặt Câu hỏi Tiêu chuẩn (3 Đáp án + 1 Tùy chọn)
- Ở mỗi bước phân tích, lấy lần lượt các **Câu hỏi tiêu chuẩn** của bước đó (ví dụ: 5 câu hỏi ở Bước 1, 7 câu hỏi ở Bước 2...).
- Sử dụng công cụ câu hỏi tương tác (`ask_question`) để trình bày câu hỏi kèm theo:
  1. **Đáp án A (Recommended):** Phương án đề xuất sát nhất với ngữ cảnh bài toán.
  2. **Đáp án B:** Phương án khả thi thứ hai (khác biệt về phạm vi hoặc cách tiếp cận).
  3. **Đáp án C:** Phương án khả thi thứ ba (tối giản hoặc mở rộng).
  4. **Tùy chọn mở (Other / Tùy chỉnh):** Cho phép người dùng nhập câu trả lời riêng hoặc yêu cầu điều chỉnh hướng phân tích.

#### Giai đoạn 2: Vòng lặp Tinh chỉnh Đáp án (Iterative Refinement Loop)
- Nếu người dùng chưa chọn được đáp án ưng ý trong 3 đáp án trên (hoặc phản hồi qua tùy chọn mở rằng các đáp án chưa sát):
  - Agent phải phân tích phản hồi của người dùng và **sinh lại 3 đáp án mới** sát hơn cho chính câu hỏi đó.
  - **Lặp đi lặp lại chu trình này** cho đến khi người dùng chốt được đáp án chính xác cho câu hỏi mới được chuyển sang câu hỏi tiếp theo.

#### Giai đoạn 3: Hiển thị Bảng Tổng hợp Q & A & Xác nhận Lần cuối (Final Q&A Gate)
- Sau khi toàn bộ các câu hỏi tiêu chuẩn của bước hiện tại đã có đáp án:
  - **CHƯA ĐƯỢC TẠO FILE `.md`.**
  - Agent phải trình bày bản **Tổng hợp Q & A** (liệt kê rõ từng Câu hỏi tiêu chuẩn và Đáp án hoàn chỉnh đã chốt) ngay trên khung chat.
  - Hỏi người dùng xác nhận lần cuối cho bản tổng hợp Q & A này:
    - **Nếu CHƯA OK:** Quay lại **Giai đoạn 1 & 2** để xây dựng và tinh chỉnh lại câu trả lời cho các câu hỏi cần sửa.
    - **Nếu ĐÃ OK:** Mới được chuyển sang Giai đoạn 4.

#### Giai đoạn 4: Khởi tạo Tài liệu Mô tả (`.md`)
- Chỉ sau khi người dùng xác nhận **"OK"** ở Giai đoạn 3, Agent mới tiến hành tạo/cập nhật file tài liệu đặc tả vào thư mục `md/analysis/` theo đúng định dạng chuẩn của bước đó.

---

### 3. Quy định Ngoại lệ khi Viết Code (Bước 7)
- **Áp dụng chu trình hỏi 3 đáp án + 1 tùy chọn:** Khi thiết kế kiến trúc module lớn, thay đổi Database Schema, API Contract hoặc refactor ảnh hưởng từ 2 file trở lên.
- **Bỏ qua (Thực thi trực tiếp):** Khi sửa lỗi nhỏ lẻ, hiển nhiên (typo, cú pháp, null check, thiếu import) hoặc khi người dùng ra lệnh trực tiếp (*"sửa luôn"*, *"fix ngay"*).
