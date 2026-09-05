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

### Severity

- **Critical**: causes data loss/corruption, a security vulnerability, or a
  crash/outage in normal use.
- **High**: incorrect behavior in a common path, a real regression, or a race
  condition likely to occur in practice.
- **Medium**: incorrect behavior only in an edge case, a missing test for a
  meaningful gap, or a performance problem with a plausible real cost.
- **Low**: maintainability or clarity issues that don't change behavior.

State the concrete failure scenario for each finding (what input or
condition triggers it) rather than a general concern, so severity is
justified by evidence, not by how significant the issue merely sounds.
