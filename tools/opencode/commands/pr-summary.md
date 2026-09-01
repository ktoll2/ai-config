---
description: Generate a reviewer-focused pull request summary from a branch comparison.
agent: plan
---

Use the `pr-summary` skill to generate a pull request summary.

Arguments: `$ARGUMENTS`

Interpret no arguments as the current branch into the repository's detected
default target. Interpret one positional branch as the target. Support
`--source <branch> --target <branch>` for an explicit comparison. If branch
resolution is not reliable, ask for the missing branch rather than assuming it.
