# Frontend – WedMate Web
ReactJS + TypeScript · Tailwind CSS · deploy Vercel
**Chủ trì:** TV3 (Phạm Anh Huy)

## Cấu trúc
```
frontend/
├── public/
├── src/
│   ├── assets/        # ảnh, icon, font
│   ├── components/    # component dùng chung (Button, Modal, Table...) – theo Design System
│   ├── layouts/       # khung layout (Sidebar, Header, Dashboard shell)
│   ├── features/      # MỖI PHÂN HỆ 1 THƯ MỤC: auth, tasks, guests, budget, vendors,
│   │                  #   wedding-plan, dashboard, admin, notifications, ai-chat
│   ├── pages/         # các trang ghép từ features
│   ├── routes/        # định tuyến + route bảo vệ theo role (Customer/Admin)
│   ├── context/       # Auth Context, ...
│   ├── hooks/         # useXxx dùng chung
│   ├── services/      # gọi REST API (axios/fetch) – KHÔNG gọi API trực tiếp trong component
│   ├── types/         # kiểu TypeScript dùng chung
│   └── utils/
└── .env.example
```
> Chưa có `package.json`/code: khởi tạo ở **WBS 1.1.3.3** (Tailwind + routing).

## Yêu cầu giao diện
- Toàn bộ **tiếng Việt**, **responsive** desktop + mobile (PF03)
- Theo wireframe/prototype Figma (link ghi trong `docs/03-design/ui-ux/README.md`)
- Chatbot: khung chat tích hợp trang kế hoạch cưới, có Quick Prompts, trạng thái loading/streaming, thông báo lỗi kết nối (WBS 1.13.1.3.x)
- Khi gọi API: luôn xử lý loading + lỗi thân thiện (PF05)
