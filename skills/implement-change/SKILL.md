---
name: implement-change
description: Use when implementing a requested feature, bug fix, or behavior change. Follows the existing architecture and conventions with minimal, focused edits.
---

# Implement Change

## Workflow

1. Understand the requested behavior.
2. Inspect the existing implementation and nearby patterns.
3. Identify the smallest appropriate change.
4. Avoid unnecessary abstractions or unrelated cleanup.
5. Preserve existing public behavior unless the task requires a change.
6. Implement the change and add or update relevant tests.
7. Build or type-check the affected code.
8. Run focused tests.
9. Inspect the final diff for accidental or unrelated changes.

Prefer existing project patterns over introducing new ones. Do not add
dependencies unless there is a clear reason. Summarize what changed and what
was verified at completion.
