# Spec Workflow — Windsurf / Cursor

Hệ thống xử lý features theo 4 bước, dùng được với bất kỳ AI IDE nào (Windsurf, Cursor, VS Code Copilot…).

## Luồng tổng quan

```
ý tưởng → [write-spec] → spec.md → [refine-spec] → spec đã verify → [launch-spec] → impl-prompt → /code → [verify-spec] → done
```

| Bước | File prompt | Mục đích | Output |
|------|------------|----------|--------|
| 1 | `prompts/01-write-spec.md` | Biến ý tưởng → spec có AC table | `.claude/specs/<feature>/spec.md` |
| 2 | `prompts/02-refine-spec.md` | Ground claims vào codebase, xóa bloat | spec đã sạch + commit |
| 3 | `prompts/03-launch-spec.md` | Compile spec → implementation prompt | prompt để dán vào chat |
| 4 | `prompts/04-verify-spec.md` | Kiểm tra code thực tế khớp spec | báo cáo pass/fail theo AC-id |

## Cách dùng trong Windsurf / Cursor

### Bước 1 — Write Spec

1. Mở chat trong IDE
2. Paste nội dung `prompts/01-write-spec.md` vào **đầu** message
3. Tiếp theo mô tả feature bạn muốn xây dựng
4. AI sẽ hỏi clarifying questions rồi viết spec vào file

**Ví dụ:**
```
[paste nội dung 01-write-spec.md]

Feature: Cho phép user đặt lịch giao hàng khi checkout
```

### Bước 2 — Refine Spec

1. Sau khi có spec draft từ bước 1
2. Paste `prompts/02-refine-spec.md` + reference file spec
3. AI sẽ đọc codebase, ground mọi claim, hỏi open questions

**Ví dụ:**
```
[paste nội dung 02-refine-spec.md]

@.claude/specs/checkout-scheduling/spec.md
```

### Bước 3 — Launch Spec

1. Sau khi spec đã được refine và sạch
2. Paste `prompts/03-launch-spec.md` + reference spec
3. AI emit một implementation prompt — **copy và dán vào chat mới** để thực hiện

### Bước 4 — Verify Spec

1. Sau khi code đã được implement
2. Paste `prompts/04-verify-spec.md` + reference spec
3. AI kiểm tra từng AC-id trong code thực, báo cáo pass/fail

---

## Template spec

Xem `templates/spec.md` để hiểu cấu trúc output mong đợi.

## Lưu spec ở đâu

Convention: `.claude/specs/<feature-slug>/spec.md`

Ví dụ:
```
.claude/specs/checkout-scheduling/spec.md
.claude/specs/user-notifications/spec.md
```

Commit spec vào git để tracking thay đổi.
