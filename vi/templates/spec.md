# {Feature Name} Spec

<!-- TL;DR: bắt buộc cho standard/full spec. 2-3 bullets ngắn. Lead bằng "breaks if missed" nếu có. -->
## TL;DR
- {Thay đổi là gì trong 1 dòng}
- {Detail quan trọng nhất mà ai đó có thể làm sai nếu không biết — cite AC-id}

---

<!-- Acceptance Criteria: contract của spec. Liệt kê EXHAUSTIVELY mọi behavior/constraint phải đúng khi done.
     Mỗi row = 1 atomic, observable end-state. ID là số thuần trong table, cite là AC-1, AC-2 ở chỗ khác.
     Default: flat table. Group chỉ khi có ≥2 obvious capability clusters. -->
## Acceptance Criteria

| AC | Criterion |
|----|-----------|
| 1  | {1 testable assertion về end state — "X is true when done"} |
| 2  | {…} |
| 3  | {Non-functional constraint nếu có: performance, security, idempotency, limit} |

---

<!-- Feature body: field definitions, behavioral rules, examples.
     Dùng table/mermaid thay prose. Bold key terms. Mỗi rule cite AC-id của nó.
     Đừng describe implementation (file paths, function names) — chỉ observable behavior. -->
## {Feature Name}

### Fields / Data

| Field | Type | Constraint | Notes |
|-------|------|-----------|-------|
| `{field}` | string | required, max 255 | {description} |

### Behavior

- **{Rule name}**: {behavioral rule} — AC-{id}
- **{Edge case}**: {what happens} — AC-{id}

### Flow

```mermaid
flowchart TD
    A[{Start}] --> B{Decision}
    B -->|Yes| C[{Action}]
    B -->|No| D[{Other action}]
```

### Watch out for

- **{Gotcha}**: Nếu implement theo cách obvious ({X}), sẽ break {Y} vì {reason}. Thay vào đó: {correct approach}.

---

<!-- UI Changes: chỉ nếu có UI thay đổi. Group theo page/area. Mỗi page cần URL. -->
## UI Changes

### {Page Name}
**URL:** [{https://example.com/path}]({https://example.com/path})

> **[Screenshot cần]:** {Mô tả chính xác: "Current form với annotations: (1) rename field X → Y, (2) remove field Z, (3) add dropdown W với options A/B/C"}

#### Changes
- {Rename/remove/add gì}

---

<!-- Data Migration: chỉ nếu existing data/logic bị ảnh hưởng. 1-2 dòng. -->
## Data Migration

{Existing data cần migrate như nào, nếu có.}

---

<!-- Boundaries: những gì implementer KHÔNG được touch.
     Chỉ boundaries specific cho change này. Convention/architecture chung → để trong project rules. -->
## Boundaries

- **{System/area}**: Không touch — {lý do ngắn}
- {…}

---

<!-- Checklist: OPTIONAL. Chỉ khi work span nhiều code areas.
     Mỗi item = 1 dòng: tên area + AC-id. KHÔNG re-describe criteria.
     Là index trỏ vào AC table, không phải copy của nó. -->
## Checklist

**{Code area — e.g. API routes}**
- [ ] {Tóm tắt work ngắn} — AC-1, AC-3

**{Code area — e.g. Database}**
- [ ] {Tóm tắt work ngắn} — AC-2

**{Code area — e.g. Frontend}**
- [ ] {Tóm tắt work ngắn} — AC-4, AC-5
