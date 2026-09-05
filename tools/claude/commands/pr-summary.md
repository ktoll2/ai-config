---
description: Generate a reviewer-focused pull request summary from a branch comparison.
argument-hint: "[target] | --source <branch> --target <branch>"
allowed-tools: Read, Grep, Glob, Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git show:*), Bash(git branch:*), Bash(git rev-parse:*), Bash(git merge-base:*), Bash(git symbolic-ref:*), Bash(git remote:*)
---

Use the `pr-summary` skill to generate a pull request summary.

Arguments: $ARGUMENTS

Interpret no arguments as the current branch into the repository's detected
default target. Interpret one positional branch as the target. Support
`--source <branch> --target <branch>` for an explicit comparison. If branch
resolution is not reliable, ask for the missing branch rather than assuming
it.
