# Refactor Skill

Guides structural code changes while preserving externally observable behavior.

Use it for renaming, simplification, restructuring, and cleanup. It identifies
the tests that protect current behavior first, adding characterization tests
if none exist, then makes incremental changes without mixing in unrelated
cleanup, and compares final behavior and diff against the original. Any
behavior change the work actually requires is treated as separate
implementation work, not folded into the refactor.

See `SKILL.md` for the complete workflow.
