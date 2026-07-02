# Example: User Avatar Upload

A complete walkthrough of the 4-step spec workflow applied to a real feature.

**Feature request**: "Allow users to upload a profile picture."

---

## Files in this example

| File | Produced by | What it shows |
| ---- | ----------- | ------------- |
| `README.md` | — | This walkthrough |
| `spec.md` | write-spec + refine-spec | The final, verified spec |
| `impl-prompt.md` | launch-spec | The prompt to paste into a new chat to implement |
| `verify-report.md` | verify-spec | The verification report after implementation |

---

## Step 1 — Write Spec

You paste `prompts/01-write-spec.md` into chat, then write:

> Allow users to upload a profile picture.

The AI runs discovery and asks:

> **Q1 (format):** Which file types should be accepted? Recommended: JPEG and PNG only (simpler validation, universal support).
>
> **Q2 (size limit):** Maximum file size? Recommended: 5 MB.
>
> **Q3 (storage):** Where should files be stored — local disk, S3, or another service? Recommended: S3 (scalable, no disk management).
>
> **Q4 (existing avatar):** When a user uploads a new avatar, what happens to the old one? Recommended: delete the old file from storage to avoid orphaned files.
>
> **Q5 (default):** What should the avatar display before a user uploads one? Recommended: their initials on a colored background (no external dependency).

You answer: JPEG/PNG, 5 MB, S3, delete old file, initials fallback.

The AI writes `spec.md` (draft) and commits it.

---

## Step 2 — Refine Spec

You paste `prompts/02-refine-spec.md` into chat, then write:

> @example/spec.md

The AI reads the codebase and finds:

- The app already has a `storage` service at `src/services/storage.ts` — the spec's claim "use S3 directly" is wrong; everything goes through this service.
- The `User` model at `src/models/user.ts` has an `avatar_url` column (confirmed), but no `avatar_storage_key` column — the spec assumed one existed for deletion. The AI flags this as an open question.
- The current max upload size in `config/uploads.ts` is set to 2 MB globally — a 5 MB avatar would require raising this limit, which the spec didn't mention. The AI adds a "Watch out for" note.

After one pass the spec is clean. The AI commits the refined version.

---

## Step 3 — Launch Spec

You paste `prompts/03-launch-spec.md` into chat, then write:

> @example/spec.md

The AI confirms the spec is ready (has AC table, Checklist, Boundaries), emits `impl-prompt.md`, and tells you to paste it into a new chat session.

---

## Step 4 — Verify Spec

After implementation, you paste `prompts/04-verify-spec.md` into chat:

> @example/spec.md

The AI reads the committed code and produces `verify-report.md`.

Result: 7/8 ACs confirmed, 1 contradicted (size limit was raised to 10 MB in code instead of 5 MB as specced). The implementer fixes it and re-runs verify.
