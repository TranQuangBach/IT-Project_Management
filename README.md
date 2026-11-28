# 💍 WedMate – Website lập kế hoạch & quản lý tiệc cưới tích hợp Chatbot AI

> Đồ án môn Quản lý dự án CNTT – Nhóm 2 – HUTECH
> Thời gian: **16/11/2026 – 08/01/2027** · 8 Sprint × 1 tuần · 5 thành viên · 800 giờ công
> Người hướng dẫn / Nhà tài trợ: ThS. Nguyễn Hữu Trung

**📌 Đọc file này trước, sau đó đọc [CONTRIBUTING.md](CONTRIBUTING.md) (quy tắc Git – bắt buộc).**

---

## 1. Dự án là gì?
WedMate giúp cặp đôi chuẩn bị đám cưới: tạo kế hoạch & đếm ngược ngày cưới, quản lý công việc, khách mời (RSVP), ngân sách, tra cứu nhà cung cấp (NCC), và hỏi **Chatbot AI (Google Gemini)** để được tư vấn theo đúng ngữ cảnh kế hoạch của họ.

## 2. Tech stack
| Tầng | Công nghệ |
|---|---|
| Frontend | ReactJS + TypeScript, Tailwind CSS, deploy **Vercel** |
| Backend | Node.js + Express, REST API (Swagger/OpenAPI), JWT + Bcrypt, Helmet/CORS |
| Database | **SQL Server**, 12 bảng chuẩn hóa |
| AI | Google Gemini API (gọi **phía server**, không gọi từ frontend) |
| Công cụ quản lý | GitHub (code), Jira (Epic = gói cấp 3; Story/Task = cấp 4–5), MS Project (lịch, baseline), Figma (UI/UX), Postman (test API) |

## 3. Cấu trúc thư mục
```
IT-Project_Management/
├── frontend/        # ReactJS + TS  (xem frontend/README.md)
├── backend/         # Node.js/Express API (xem backend/README.md)
├── database/        # Script schema, migration, dữ liệu mẫu (seed)
├── docs/            # TOÀN BỘ tài liệu dự án (QLDA, BA, thiết kế, test, báo cáo)
├── tests/           # Postman collection, kịch bản test tự động (nếu có)
├── scripts/         # Script tiện ích (setup, seed, deploy)
└── .github/         # PR template, Issue template, CODEOWNERS
```
Chi tiết `docs/`:
| Thư mục | Nội dung | Phụ trách chính |
|---|---|---|
| `01-project-management/` | Charter, WBS (docx + xlsx), Baseline, RACI, Risk register, báo cáo EVM | TV1 |
| `02-requirements/` | Scope Statement, SRS, Use Case UC01–UC13, RTM, Product Backlog | TV4 |
| `03-design/` | `architecture/`, `erd/`, `api/` (Swagger), `ui-ux/` (link Figma, wireframe) | TV2, TV5 |
| `04-testing/` | Test Plan, Test Cases, Test Report, kịch bản test chatbot (30 kịch bản) | TV5 |
| `05-deployment/` | Hướng dẫn cài đặt, cấu hình môi trường, deploy Vercel/Cloud | TV1, TV2 |
| `06-final-report/` | Báo cáo đồ án (10 chương), slide bảo vệ, video demo | Cả nhóm |
| `meetings/` | Biên bản họp, Sprint Planning/Review/Retro | TV4 |

## 4. Phân hệ chức năng ↔ yêu cầu ↔ Sprint
| Phân hệ (thư mục) | Yêu cầu | Sprint | Backend | Frontend |
|---|---|---|---|---|
| `auth` – Tài khoản, phân quyền | YC01 | S3 | TV2 | TV3 |
| `wedding-plan` – Kế hoạch, đếm ngược | YC02 | S4 | TV2 | TV3 |
| `tasks` – Quản lý công việc | YC04 | S4 | TV2 | TV3 |
| `vendors` – Nhà cung cấp | YC07 | S4–S5 | TV1 (S4), TV2 (S5) | TV3 |
| `guests` – Khách mời, RSVP | YC05 | S5 | TV2 | TV3 |
| `dashboard` – Tổng quan | YC03 | S5 | TV1 | TV1 |
| `budget` – Ngân sách | YC06 | S6 | TV2 | TV3 |
| `admin` – Quản trị | YC09 | S6 | TV2 | TV1 |
| `notifications` – Thông báo | YC10 (Should) | S6 | TV2 | TV1 |
| `ai-chat` – Chatbot AI | YC08 | S6–S7 | TV2 (context, API chat) · TV3 (service Gemini) · TV4 (prompt) | TV3 |

Yêu cầu phi chức năng: **PF01** phản hồi ≤ 3s · **PF02** bảo mật & phân quyền · **PF03** tiếng Việt + responsive · **PF04** kiến trúc/validation 2 lớp/CSDL 12 bảng · **PF05** xử lý lỗi thân thiện, demo online.

## 5. Đội ngũ
| Mã | Họ tên | Vai trò | Phạm vi code chính |
|---|---|---|---|
| TV1 | Trần Quang Bách | **PM** & Fullstack | `docs/01-project-management`, dashboard, admin FE, middleware, deploy |
| TV2 | Đỗ Thư Kỳ | **Dev Lead** & Backend | `backend/`, `database/`, review PR kỹ thuật |
| TV3 | Phạm Anh Huy | Frontend & AI Integration | `frontend/`, `backend/src/services/gemini/` (gọi Gemini phía server), khung chat AI |
| TV4 | Trần Thị Yến Nhi | **BA** | `docs/02-requirements`, dữ liệu mẫu NCC, **prompt chatbot** |
| TV5 | Triệu Đoan Kỳ | UI/UX & **Tester** | Figma, `docs/04-testing`, `tests/` |

Mỗi người làm **20 giờ/Sprint** (4h/ngày). Việc của từng người nằm trong file WBS (`docs/01-project-management/WBS_WedMate_ChatbotAI.xlsx`, cột *Tài nguyên*).

## 6. Lịch & mốc (Milestones) – Git tag tương ứng
| Mốc | Ngày | Nội dung | Git tag |
|---|---|---|---|
| M1 | 20/11/2026 | Duyệt Tôn chỉ | – |
| M2 | 27/11/2026 | Duyệt kế hoạch, lưu Baseline | – |
| M3 | 04/12/2026 | Demo v0.1 (Tài khoản + khung UI) | `v0.1.0` |
| M3b | 11/12/2026 | Demo S4 (Kế hoạch + Công việc) | `v0.1.x` |
| M4 | 18/12/2026 | Giữa kỳ, Demo v0.2 | `v0.2.0` |
| M4b | 26/12/2026 | Demo S6 (Ngân sách, Admin, khung AI) | `v0.2.x` |
| M5 | 02/01/2027 | v1.0-rc + UAT (9/9 module trên Vercel) | `v1.0.0-rc.1` |
| M6 | 08/01/2027 | Bảo vệ & bàn giao | `v1.0.0` |

Nghỉ Tết Dương lịch 01/01/2027; làm bù Thứ Bảy 26/12/2026.

## 7. Chạy dự án ở máy local
> Các bước dưới sẽ chạy được dần khi code được đẩy lên (Sprint 3 trở đi). Chi tiết ở README của từng thư mục.
```bash
git clone https://github.com/TranQuangBach/IT-Project_Management && cd IT-Project_Management
git checkout develop

# 1) Database: tạo DB "WedMate" trên SQL Server, chạy script trong database/schema (xem database/README.md)
# 2) Backend
cd backend && cp .env.example .env   # điền thông tin thật
npm install && npm run dev
# 3) Frontend
cd ../frontend && cp .env.example .env
npm install && npm run dev
```

## 8. Quy tắc quan trọng (tóm tắt)
1. **Không code trực tiếp trên `main` / `develop`.** Mọi thay đổi qua Pull Request.
2. **Không commit** `.env`, API key, mật khẩu. Key Gemini xin PM/Dev Lead, chia sẻ qua kênh riêng.
3. Mỗi PR gắn **mã WBS + Jira key**, có ít nhất **1 reviewer** (xem `CODEOWNERS`).
4. Đổi phạm vi (thêm/bớt tính năng) sau M2 → **phải qua CCB**, báo PM, không tự làm thêm.
5. Task chậm/vướng → báo trong kênh nhóm **trong ngày**, đừng đợi họp Sprint.
6. Chatbot **chỉ được tư vấn NCC có trong CSDL** (grounding) – không để AI bịa dữ liệu.

## 9. Liên hệ
PM: Trần Quang Bách (TV1) – hỏi về tiến độ, phạm vi, lịch họp, quyền truy cập Jira/GitHub/MS Project.
Kỹ thuật: Đỗ Thư Kỳ (TV2) – hỏi về kiến trúc, API, database, Git.
