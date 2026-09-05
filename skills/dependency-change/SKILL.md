---
name: dependency-change
description: Use when adding, removing, replacing, upgrading, or downgrading a dependency or package, including version bumps, lock file updates, and migrations.
---

# Dependency Changes

## Workflow

1. Determine why the dependency change is needed.
2. Check whether existing dependencies or platform functionality suffice.
3. Identify where the dependency is used.
4. For a new dependency, check its license compatibility, maintenance
   status, and any known security advisories before adding it.
5. Evaluate compatibility and migration impact.
6. Review release or migration notes when upgrading.
7. Prefer the smallest necessary version change.
8. Update dependency declarations and lock files consistently.
9. Build the affected project and run relevant tests.
10. Check for deprecated or changed APIs.

Do not add a dependency solely to avoid a small amount of straightforward
code. Call out significant transitive dependencies, compatibility concerns, or
migration requirements.

## Reporting

State what changed (package, old and new version or replacement), why, and
what was verified (build, tests, deprecated-API check). Flag any transitive
dependency, license, or migration concern found along the way even if it
didn't block the change.
