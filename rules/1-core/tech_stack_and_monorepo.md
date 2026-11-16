## STACK CÔNG NGHỆ & CẤU TRÚC MONOREPO

### 1. Stack Công nghệ
- **Frontend:** Next.js 16 (App Router, TypeScript, TailwindCSS v3+)
- **Backend:** NestJS 11 (TypeScript, Mongoose ODM)
- **Database:** MongoDB
- **Ngôn ngữ:** TypeScript bắt buộc cho cả Frontend và Backend
- **Trình quản lý gói (Package Manager):** Bắt buộc dùng **`pnpm`** cho toàn dự án (**CẤM** dùng `npm` hoặc `yarn`; chỉ duy trì `pnpm-lock.yaml`, tuyệt đối không sinh `package-lock.json` hay `yarn.lock`).

### 2. Cấu trúc Monorepo & Quy tắc File
- `frontend/` và `backend/` đặt ngang hàng trong workspace, quản lý tập trung qua `pnpm-workspace.yaml` ở thư mục gốc.
- Mọi thao tác cài đặt và chạy lệnh bắt buộc dùng `pnpm`: `pnpm install`, `pnpm add <pkg>`, `pnpm dlx <cli>` (thay cho `npx`), và `pnpm --filter <workspace> <script>`.
- File `.env` đặt ở root/module, nằm trong `.gitignore` (luôn kèm `.env.example` mẫu, không hardcode secrets).
- Comment tiếng Việt cho logic nghiệp vụ, tiếng Anh cho technical docs.
- **Giới hạn độ dài:** Mỗi file tối đa **300 dòng code** — vượt quá phải tách sub-component hoặc helper/service.

