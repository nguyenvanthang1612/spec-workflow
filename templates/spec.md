# {Feature Name} Spec

<!-- TL;DR: required for standard/full specs. 2-3 short bullets. Lead with "breaks if missed" risk if any. -->
## TL;DR
- {What the change is in one line}
- {The most important detail someone might get wrong without a heads-up — cite AC-id}

---

<!-- Acceptance Criteria: the spec's contract. List EXHAUSTIVELY every behavior/constraint that must hold when done.
     Each row = 1 atomic, observable end-state. ID is a bare number in the table; cited as AC-1, AC-2 elsewhere.
     Default: flat table. Group only when there are ≥2 obvious capability clusters. -->
## Acceptance Criteria

| AC | Criterion |
| -- | --------- |
| 1  | {1 testable assertion about the end state — "X is true when done"} |
| 2  | {…} |
| 3  | {Non-functional constraint if applicable: performance, security, idempotency, limit} |

---

<!-- Feature body: field definitions, behavioral rules, examples.
     Use tables/mermaid instead of prose. Bold key terms. Each rule cites its AC-id.
     Do not describe implementation (file paths, function names) — only observable behavior. -->
## {Feature Name}

### Fields / Data

| Field | Type | Constraint | Notes |
| ----- | ---- | ---------- | ----- |
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

- **{Gotcha}**: If implemented the obvious way ({X}), it will break {Y} because {reason}. Instead: {correct approach}.

---

<!-- UI Changes: only if there are UI changes. Group by page/area. Each page needs a URL. -->
## UI Changes

### {Page Name}
**URL:** [{https://example.com/path}]({https://example.com/path})

> **[Screenshot needed]:** {Describe exactly: "Current form with annotations: (1) rename field X → Y, (2) remove field Z, (3) add dropdown W with options A/B/C"}

#### Changes
- {What to rename/remove/add}

---

<!-- Data Migration: only if existing data/logic is affected. 1-2 lines. -->
## Data Migration

{How existing data needs to be migrated, if at all.}

---

<!-- Boundaries: what the implementer must NOT touch.
     Only boundaries specific to this change. General conventions/architecture → keep in project rules. -->
## Boundaries

- **{System/area}**: Do not touch — {brief reason}
- {…}

---

<!-- Checklist: OPTIONAL. Only when work spans multiple code areas.
     Each item = 1 line: area name + AC-id. Do NOT re-describe criteria.
     This is an index pointing at the AC table, not a copy of it. -->
## Checklist

**{Code area — e.g. API routes}**
- [ ] {Brief summary of work} — AC-1, AC-3

**{Code area — e.g. Database}**
- [ ] {Brief summary of work} — AC-2

**{Code area — e.g. Frontend}**
- [ ] {Brief summary of work} — AC-4, AC-5
