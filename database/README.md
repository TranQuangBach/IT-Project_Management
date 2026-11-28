# Database – SQL Server (12 bảng chuẩn hóa)
**Chủ trì:** TV2

```
database/
├── schema/       # script tạo bảng (001_create_tables.sql ...) – WBS 1.5.2.1
├── migrations/   # mọi thay đổi schema SAU khi đã chạy: đánh số 002_, 003_ ...
└── seeds/        # dữ liệu mẫu: danh mục dịch vụ, tài khoản demo, ≥ 40 NCC (TV4 chuẩn hóa)
```

## Quy tắc
1. ERD & Data Dictionary là nguồn chuẩn: `docs/03-design/erd/` (WBS 1.3.3.2). Code/DB phải khớp ERD.
2. **Không sửa DB chung bằng tay.** Muốn đổi cấu trúc → tạo file migration mới, mở PR, báo TV2.
3. Dữ liệu seed không chứa thông tin cá nhân thật; tài khoản demo dùng mật khẩu đã hash (Bcrypt).
4. Seed NCC (≥ 40 nhà cung cấp: nhà hàng, studio, váy cưới, trang trí) do **TV4** chuẩn hóa dạng CSV/JSON/SQL trong `seeds/`; chatbot chỉ được gợi ý NCC có trong bảng này.
