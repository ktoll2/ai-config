# Testing Rules

- Build or type-check affected code before considering a change done.
- Run the most relevant focused tests first, then broader tests when
  practical.
- Inspect failures rather than assuming they're unrelated; only treat one as
  flaky after actually reproducing the inconsistency, not on first guess.
- Never skip, delete, or weaken a test to make a run pass; fix the cause or
  flag it instead.
- For bug fixes, add a test that fails before the fix and passes after,
  where feasible.
- Report exactly what was and was not verified; never claim a test passed
  without having actually run it.
