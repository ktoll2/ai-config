---
name: dependency-change
description: Use when adding, removing, replacing, upgrading, or downgrading a dependency or package, including version bumps, lock file updates, and migrations.
---

# Dependency Changes

## Workflow

1. Determine why the dependency change is needed.
2. Check whether existing dependencies or platform functionality suffice.
3. Identify where the dependency is used.
4. Evaluate compatibility and migration impact.
5. Review release or migration notes when upgrading.
6. Prefer the smallest necessary version change.
7. Update dependency declarations and lock files consistently.
8. Build the affected project and run relevant tests.
9. Check for deprecated or changed APIs.

Do not add a dependency solely to avoid a small amount of straightforward
code. Call out significant transitive dependencies, compatibility concerns, or
migration requirements.
