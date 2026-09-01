---
name: investigate-bug
description: Use when diagnosing a bug, error, failing test, regression, or other unexpected behavior before changing code. Finds the root cause from evidence rather than guesswork.
---

# Bug Investigation

## Workflow

1. Understand reported and expected behavior.
2. Locate relevant entry points and code paths.
3. Trace the behavior and reproduce it when practical.
4. Gather evidence before forming conclusions.
5. Identify likely root causes and distinguish facts from hypotheses.
6. Determine the smallest reasonable fix and tests that should prove it.

## Output

Report observed behavior, relevant code path, confirmed root cause, unresolved
hypotheses, recommended fix, and tests to add or change. Do not modify code
during investigation unless explicitly asked.
