# Implementation Prompt (output of launch-spec)

> This file is the output of step 3 (launch-spec).
> Copy everything inside the box below and paste it into a **new chat session** to implement.

---

```
## Goal

Implement the User Avatar Upload feature per the spec at `@spec-workflow/example/spec.md`.

Read the spec in full, then implement every acceptance criterion. The spec has been verified by refine-spec and is ready to implement.

## Acceptance Criteria to satisfy

| AC | Criterion |
| -- | --------- |
| 1  | A user can upload a JPEG or PNG file as their avatar from the account settings page |
| 2  | Files larger than 5 MB are rejected before upload with a clear error message |
| 3  | Files of any type other than JPEG or PNG are rejected before upload with a clear error message |
| 4  | On successful upload, the new avatar is immediately visible on the user's profile and in the nav bar |
| 5  | When a user replaces an existing avatar, the previous file is deleted from S3 |
| 6  | Users who have never uploaded an avatar see their initials on a colored background in all avatar positions |
| 7  | The upload request is authenticated — unauthenticated requests are rejected with 401 |
| 8  | The global upload size limit in config is raised to at least 5 MB to allow avatar uploads |

## Checklist

**API — `src/routes/users/`**
- [ ] Add `POST /api/users/me/avatar` route with auth middleware — AC-1, AC-7
- [ ] Validate MIME type and file size server-side — AC-2, AC-3
- [ ] Call `storage.ts` upload, then delete old key if present, then update DB — AC-4, AC-5

**Database — `src/models/`**
- [ ] Migration: add `avatar_storage_key` column to `users` — AC-5
- [ ] Update `User` model to include `avatar_storage_key` — AC-5

**Config — `config/uploads.ts`**
- [ ] Raise global (or avatar-scoped) upload limit to ≥ 5 MB — AC-8

**Frontend — `src/components/`**
- [ ] Avatar component: circle crop, initials fallback, deterministic color — AC-6
- [ ] Settings page: file picker, upload handler, error/loading states — AC-1, AC-2, AC-3
- [ ] Nav bar: swap placeholder icon with Avatar component — AC-4, AC-6

## Boundaries — do NOT touch

- **`storage.ts` is the only S3 interface**: do not import the AWS SDK or call S3 directly.
- **Do not change other upload endpoints**: only the avatar endpoint gets the raised size limit.
- **Do not touch the `auth` middleware**: reuse existing middleware as-is.

## Done gate

You are NOT done until:
1. Every acceptance criterion (AC-1 through AC-8) is satisfied
2. verify-spec run against `spec-workflow/example/spec.md` returns zero contradicted claims

## Commit cadence

Commit after each Checklist section verifies clean. Each commit is scoped to the files changed; the message cites the relevant AC-ids. Example: `feat(avatar): add upload endpoint and storage key migration — AC-1,AC-5,AC-7,AC-8`. Do not push.

## Artifact hygiene

Code, comments, tests, and docs must stand alone — no AC-ids, spec filenames, or phase numbers in delivered code. Name every function, variable, class, and test for what it does. No background context that doesn't help a future maintainer act.
```
