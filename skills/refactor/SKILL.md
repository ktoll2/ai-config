---
name: refactor
description: Use when refactoring, restructuring, renaming, simplifying, or cleaning up code while preserving externally observable behavior.
---

# Refactoring

## Workflow

1. Understand current responsibilities and behavior.
2. Identify tests that protect that behavior; add characterization tests if
   necessary.
3. Define the structural problem being addressed.
4. Make incremental changes without mixing unrelated cleanup.
5. Preserve public interfaces unless explicitly allowed to change them.
6. Run relevant tests and compare final behavior and diff with the original.

Prefer simpler code and clearer ownership over abstraction for its own sake.
Treat required behavior changes as separate implementation work.
