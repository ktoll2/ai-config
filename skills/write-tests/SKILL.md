---
name: write-tests
description: Use when writing, adding, or improving tests, unit tests, or test coverage, whether for new behavior, existing code, or a bug fix.
---

# Write Tests

## Workflow

1. Determine the behavior being protected.
2. Inspect existing tests for conventions and helpers.
3. Prefer behavioral tests over implementation-detail tests.
4. Cover the normal case, then important boundary and failure cases.
5. Keep tests deterministic and avoid unnecessary mocking or duplicate
   coverage.
6. Run the smallest relevant test set and confirm it exercises the intended
   behavior.

For bug fixes, prefer a test that fails before the fix and passes afterward.
