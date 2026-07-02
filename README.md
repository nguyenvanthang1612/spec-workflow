# Spec Workflow — Windsurf / Cursor

A 4-step feature processing system that works with any AI IDE (Windsurf, Cursor, VS Code Copilot…).

> Vietnamese version: `vi/README.md`

## Overview

```
idea → [write-spec] → spec.md → [refine-spec] → verified spec → [launch-spec] → impl-prompt → implement → [verify-spec] → done
```

| Step | Prompt file | Purpose | Output |
| ---- | ----------- | ------- | ------ |
| 1 | `prompts/01-write-spec.md` | Turn idea → spec with AC table | `.claude/specs/<feature>/spec.md` |
| 2 | `prompts/02-refine-spec.md` | Ground claims in codebase, remove bloat | clean spec + commit |
| 3 | `prompts/03-launch-spec.md` | Compile spec → implementation prompt | prompt to paste into chat |
| 4 | `prompts/04-verify-spec.md` | Verify real code matches spec | pass/fail report per AC-id |

## How to use in Windsurf / Cursor

### Step 1 — Write Spec

1. Open chat in the IDE
2. Paste the contents of `prompts/01-write-spec.md` at the **top** of your message
3. Then describe the feature you want to build
4. The AI will ask clarifying questions, then write the spec to a file

**Example:**
```
[paste contents of 01-write-spec.md]

Feature: Allow users to schedule a delivery time during checkout
```

### Step 2 — Refine Spec

1. After you have a spec draft from step 1
2. Paste `prompts/02-refine-spec.md` + reference the spec file
3. The AI will read the codebase, ground every claim, and ask about open questions

**Example:**
```
[paste contents of 02-refine-spec.md]

@.claude/specs/checkout-scheduling/spec.md
```

### Step 3 — Launch Spec

1. After the spec has been refined and is clean
2. Paste `prompts/03-launch-spec.md` + reference the spec
3. The AI emits an implementation prompt — **copy and paste it into a new chat** to implement

### Step 4 — Verify Spec

1. After the code has been implemented
2. Paste `prompts/04-verify-spec.md` + reference the spec
3. The AI checks each AC-id against real code and reports pass/fail

---

## Spec template

See `templates/spec.md` for the expected output structure.

## Where to save specs

Convention: `.claude/specs/<feature-slug>/spec.md`

Examples:
```
.claude/specs/checkout-scheduling/spec.md
.claude/specs/user-notifications/spec.md
```

Commit the spec to git to track changes.
