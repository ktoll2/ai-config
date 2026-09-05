---
name: refactor
description: Use when refactoring, restructuring, renaming, simplifying, or cleaning up code while preserving externally observable behavior.
---

# Refactoring

## Workflow

1. Understand current responsibilities and behavior.
2. Identify tests that protect that behavior; add characterization tests if
   necessary.
3. Define the structural problem being addressed: duplication, an
   overloaded module, unclear ownership, a leaky abstraction, or similar.
4. Make incremental changes without mixing unrelated cleanup, keeping each
   step small enough to review and verify on its own.
5. Preserve public interfaces unless explicitly allowed to change them.
6. Run relevant tests and compare final behavior and diff with the original.

Prefer simpler code and clearer ownership over abstraction for its own sake.
Treat required behavior changes as separate implementation work: if the task
turns out to need one, stop and call it out rather than folding it in.
