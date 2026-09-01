---
name: pr-summary
description: Use when generating a pull request summary from a Git branch comparison, diff, commits, or PR context. Resolves source and target branches safely and produces a concise reviewer-focused summary.
---

# Pull Request Summary

Generate a clear, concise, technically useful pull request summary for
engineers reviewing a change. Explain what changed, why it changed when known,
how the solution works when useful, and how it was validated.

Do not reproduce the diff, list changed files, or generate a file tree.

## Source of Truth

Base the summary only on the current diff, changed files, relevant source-side
commits, user-provided ticket or issue context, code and documentation needed
to understand the change, and available test execution results. Do not infer
intent, requirements, behavior, or test results without support. If the reason
is unclear, describe what the change accomplishes instead.

## Branch Selection

The source branch contains the proposed changes; the target branch is where it
will be merged.

- With no explicit source, use the currently checked-out branch. If HEAD is
  detached, request a source branch.
- With an explicit source, use it even if another branch is checked out.
- With an explicit target, use it.
- Without a target, determine the repository's configured default branch from
  its remote HEAD when available. Do not assume `main` or `master`. If it
  cannot be determined reliably, request the target branch.
- With one positional argument, treat it as the target branch.
- With `--source <branch>` and `--target <branch>`, use the supplied branches.
- Verify both references before analysis.

Analyze the effective PR comparison `target...source`, which describes changes
introduced by the source since its merge base with the target. Do not summarize
changes made independently to the target after divergence.

All Git operations are read-only. Do not checkout, switch, create, merge,
rebase, cherry-pick, commit, amend, pull, push, reset, or modify the working
tree.

## Analysis Process

1. Resolve and verify source and target branches.
2. Identify their merge base and inspect `target...source`.
3. Inspect source-side commits when they help explain intent.
4. Determine the primary purpose, supported motivation, and substantive changes.
5. Identify meaningful behavior, contract, architecture, data flow, error
   handling, security, concurrency, caching, messaging, configuration,
   dependency, observability, and test changes.
6. Check for externally visible or breaking changes, deployment or migration
   requirements, risks, tradeoffs, and reviewer-sensitive areas.
7. Separate test coverage visible in the change from tests known to have run.
8. Ignore formatting-only and mechanical edits unless they are a significant
   purpose of the PR.

Pay particular attention to REST and gRPC contracts, request and response
models, database schemas, message and persistent-data formats, configuration
keys, environment variables, authentication, authorization, and external
integrations.

## Output

Always make the first line the resolved direction, exactly:

```text
target <-- source
```

The left side is always the target; do not reverse or omit it.

Always include these sections:

```md
{target} <-- {source}

## Summary

{two to four sentence overview}

## Changes

- {logical change}

## Testing

- {tests added, modified, or executed}
```

Include these sections only when supported and useful: `Motivation / Context`,
`Technical Approach`, `Breaking Changes`, `Deployment / Migration`, `Risks /
Considerations`, `Reviewer Focus`, and `Related Work`. Never add an optional
section solely to state “None”, “N/A”, or equivalent.

### Section Rules

- **Summary:** state the result and scope without duplicating Changes or
  enumerating files.
- **Changes:** group related functional, behavioral, architectural, contract,
  and data-flow changes. Prefer logical areas over file-by-file descriptions.
- **Technical Approach:** explain significant design, persistence, messaging,
  concurrency, caching, or error-handling decisions when they help review.
- **Testing:** distinguish added or modified coverage from tests actually run.
  Never claim tests passed without explicit results. If testing cannot be
  established, write `- Not determined from the available changes.`
- **Breaking Changes:** include only potential or confirmed externally visible
  incompatibilities, affected consumers, and required actions when known.
- **Deployment / Migration:** include only required migrations, configuration,
  flags, dependency actions, ordering, or manual steps.
- **Risks / Considerations** and **Reviewer Focus:** include only meaningful,
  supported risks or areas needing closer scrutiny.
- **Related Work:** include only explicitly known tickets, PRs, documentation,
  prerequisites, or follow-up work.

For large PRs, organize changes by logical area. For small PRs, do not expand
the output merely to populate sections. Write concisely, precisely, and for an
experienced engineer. Use active voice and bullets for independent changes.

## Final Review

Before returning the summary, confirm the branch direction and resolved refs
are correct; claims are supported; changes are logically grouped; public,
breaking, deployment, and testing considerations are accurately represented;
and empty optional sections are omitted.
