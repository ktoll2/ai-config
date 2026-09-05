# Skills

Repeatable workflows, one directory per skill. Each skill pairs a `SKILL.md` (the agent-facing workflow: frontmatter `name`/`description` plus the actual steps) with a `README.md` (a short human-facing summary of what it does and when to reach for it). The `SKILL.md` frontmatter format is already native to more than one AI tool, so tool adapters generally load this directory directly with no translation - see the relevant `tools/<tool>/README.md` for exactly how a given tool wires it in.

## What's here

| Skill | Use it when... |
|---|---|
| [`implement-change/`](implement-change/) | Implementing a requested feature, bug fix, or behavior change. |
| [`investigate-bug/`](investigate-bug/) | Diagnosing a bug, error, failing test, regression, or other unexpected behavior before changing code. |
| [`code-review/`](code-review/) | Reviewing code changes, a PR, or a diff for correctness, regressions, security, and missing tests. |
| [`refactor/`](refactor/) | Refactoring, restructuring, renaming, or cleaning up code while preserving behavior. |
| [`write-tests/`](write-tests/) | Writing, adding, or improving tests for new or existing behavior. |
| [`dependency-change/`](dependency-change/) | Adding, removing, upgrading, or downgrading a dependency, including lock file updates. |
| [`performance-investigation/`](performance-investigation/) | Investigating slow execution, high CPU/memory, or latency problems. |
| [`pr-summary/`](pr-summary/) | Generating a pull request summary from a branch comparison, diff, or commits. |

## Adding a skill

1. Create `skills/<skill-name>/SKILL.md` with `name` and `description` frontmatter - the description is what a tool uses to decide when to invoke the skill automatically, so state concretely what kind of task it covers ("Use when...").
2. Add `skills/<skill-name>/README.md` with a short human-facing summary; keep it brief and point to `SKILL.md` for the actual workflow, following the existing skills' pattern.
3. A skill needs no tool-specific adapter to be usable - every adapter already loads `skills/` as-is. A skill only needs an addition under a given `tools/<tool>/` if that tool should also reach it through an explicit command or a dedicated agent with its own restricted tool access - see that tool's adapter README for whether and how it does either.
