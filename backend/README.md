# Backend – WedMate API
Node.js + Express · SQL Server · JWT/Bcrypt · Helmet/CORS · Swagger/OpenAPI
**Chủ trì:** TV2 (Đỗ Thư Kỳ)

## Cấu trúc
```
backend/
├── src/
│   ├── config/        # đọc .env, kết nối SQL Server, cấu hình Gemini
│   ├── middlewares/   # auth (JWT), phân quyền role, validation, xử lý lỗi tập trung
│   ├── modules/       # MỖI PHÂN HỆ 1 THƯ MỤC (xem modules/README.md)
│   ├── routes/        # gom route của các module -> /api/*
│   ├── services/      # dịch vụ dùng chung
│   │   └── gemini/    # client gọi Google Gemini API, hạn mức token (TV3 – WBS 1.11.3.1)
│   └── utils/
├── tests/             # unit/integration test phía backend
└── .env.example       # mẫu biến môi trường (copy -> .env)
```
> Chưa có `package.json`/code: TV2 khởi tạo ở **WBS 1.1.3.1** / bắt đầu code Sprint 3.

## Quy ước API
- Prefix `/api/<module>`; JSON `{ success, data, message }`
- Auth: `Authorization: Bearer <JWT>`; 2 role: `Customer`, `Admin`
- Tài liệu API: Swagger/OpenAPI lưu tại `docs/03-design/api/` (WBS 1.3.3.3)

## Biến môi trường
Xem `.env.example`. **Không commit `.env`.**
