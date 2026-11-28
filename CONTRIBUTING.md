# Hướng dẫn làm việc nhóm (Git workflow & quy ước)

> ⚠️ Các quy ước dưới đây là **bản đề xuất của PM** (WBS 1.1.1.4 giao TV2 chốt quy ước nhánh/commit/DoD). TV2 xem lại và chỉnh trong Sprint 3 nếu cần; sau khi chốt, mọi người tuân thủ.

## 1. Mô hình nhánh

```
main     ← chỉ chứa bản đã duyệt/demo/release; có Git tag. Chỉ PM merge.
 └─ develop   ← nhánh tích hợp hằng ngày. Merge qua PR.
      ├─ feature/<module>-<mô-tả-ngắn>   ví dụ: feature/auth-login-api
      ├─ fix/<module>-<mô-tả-ngắn>       ví dụ: fix/tasks-filter-overdue
      ├─ docs/<mô-tả>                    ví dụ: docs/update-srs-uc05
      └─ chore/<mô-tả>                   ví dụ: chore/eslint-config
```

- Tên nhánh: chữ thường, dùng dấu `-`, `<module>` lấy từ danh sách phân hệ (auth, tasks, guests, budget, vendors, dashboard, wedding-plan, admin, notifications, ai-chat).
- Cuối mỗi Sprint (hoặc tại mốc Demo): PM merge `develop` → `main` và gắn tag (xem bảng mốc ở README).
- Xóa nhánh sau khi PR được merge.

## 2. Quy trình làm một task

1. Nhận task (Jira) → ghi rõ **mã WBS**.
2. `git checkout develop && git pull`
3. `git checkout -b feature/<module>-<mô-tả>`
4. Code + commit nhỏ, thường xuyên.
5. Trước khi mở PR: `git pull origin develop` (hoặc rebase) và giải quyết conflict ở máy mình.
6. Push → mở **Pull Request vào `develop`**, điền đủ template.
7. Reviewer review trong **24h** (ngày làm việc). Sửa theo góp ý → được approve → **người tạo PR hoặc reviewer** bấm _Squash and merge_.
8. Kéo Jira card sang _Done_ khi đạt Definition of Done.

## 3. Quy ước commit (Conventional Commits)

```
<type>(<module>): <mô tả ngắn, thể mệnh lệnh>

ví dụ:
feat(auth): add login API with JWT
fix(tasks): correct overdue filter by due date
docs(srs): update use case UC05
test(budget): add cases for over-budget warning
```

`type`: `feat` · `fix` · `docs` · `test` · `refactor` · `style` · `chore`
Mô tả bằng tiếng Việt không dấu

## 4. Review PR

| Thay đổi ở              | Reviewer bắt buộc                        |
| ----------------------- | ---------------------------------------- |
| `backend/`, `database/` | TV2 (Dev Lead)                           |
| `frontend/`             | TV3 hoặc TV2                             |
| prompt chatbot          | TV4 + TV2                                |
| `docs/`                 | Người phụ trách thư mục (xem CODEOWNERS) |

Người viết code **không tự approve PR của mình**.

## 5. Definition of Done (đề xuất)

Một task chỉ "xong" khi:

- [ ] Chạy đúng ở local, không lỗi console/terminal
- [ ] Có validation ở cả FE và BE (PF04)
- [ ] Xử lý lỗi thân thiện, không lộ stack trace ra UI (PF05)
- [ ] Giao diện tiếng Việt, hiển thị tốt trên desktop & mobile (PF03)
- [ ] Mật khẩu/token/key không bị lộ; kiểm tra phân quyền Customer/Admin (PF02)
- [ ] Đã cập nhật Swagger/docs nếu đổi API
- [ ] PR được approve và merge vào `develop`
- [ ] Tester (TV5) đã có test case tương ứng

## 6. Quy ước code

- **Frontend**: component `PascalCase.tsx`; hook `useXxx.ts`; mỗi phân hệ nằm trong `src/features/<module>/`, phần dùng chung ở `components/`, `hooks/`, `utils/`. Gọi API qua `services/`, **không** `fetch` rải rác trong component.
- **Backend**: mỗi phân hệ trong `src/modules/<module>/` gồm `*.routes.js|ts`, `*.controller`, `*.service`, `*.validation`. Controller mỏng, logic ở service. Lỗi đi qua middleware xử lý lỗi tập trung.
- **API**: tiền tố `/api/<module>`, trả JSON thống nhất `{ success, data, message }`; đặt tên số nhiều (`/api/tasks`).
- **Database**: không sửa schema trực tiếp trên DB chung – tạo file migration trong `database/migrations/` (đánh số `001_...sql`) và báo TV2.
- **Chatbot/AI**: chỉ gọi Gemini từ backend; prompt lưu trong `backend/src/modules/ai-chat/prompts/` (TV4 chủ trì, đổi prompt phải qua PR).

## 7. Thay đổi phạm vi (CCB)

Sau mốc M2 (27/11/2026), việc **thêm/bớt/đổi** tính năng phải: (1) báo PM → (2) PM ghi nhận Change Request trong `docs/01-project-management/` → (3) CCB duyệt → (4) cập nhật WBS/Backlog. Không tự ý làm thêm ngoài WBS.

## 8. Họp & báo cáo

- Mỗi Sprint: Planning (đầu tuần) – Review & Retrospective (cuối tuần), do TV1 chủ trì; biên bản TV4 lưu ở `docs/meetings/` (đặt tên `YYYY-MM-DD_sprintN_planning.md`).
- Cập nhật Jira hằng ngày (trạng thái + giờ thực tế) để PM tính tiến độ & EVM.
