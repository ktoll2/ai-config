---
name: code-review
description: Use when reviewing code changes, a PR, pull request, or diff. Checks correctness, regressions, security, concurrency, compatibility, performance, maintainability, and missing tests, with findings reported by severity.
---

# Code Review

Review the requested changes or current diff as an independent reviewer.

## Workflow

1. Inspect the complete change.
2. Read enough surrounding code to understand its context.
3. Determine the intended behavior.
4. Look for defects and unintended behavioral changes.
5. Consider edge cases and failure paths.
6. Check concurrency and asynchronous behavior where relevant.
7. Look for performance or resource problems.
8. Check API and data compatibility.
9. Evaluate test coverage.
10. Avoid stylistic comments unless they materially affect maintainability.

## Findings

Prioritize correctness, data loss or corruption, security, concurrency,
compatibility, performance, maintainability, and missing tests. Report
concrete findings first and order them by severity. Do not modify files unless
explicitly asked.
