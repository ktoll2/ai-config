# Pull Request Summary Skill

Produces concise, reviewer-focused pull request summaries from a read-only
`target...source` Git comparison.

It supports the current branch into the detected default target, an explicit
target positional argument, or explicit `--source` and `--target` arguments,
and never checks out, merges, or otherwise modifies the working tree.

The output always starts with the resolved `target <-- source` direction,
followed by Summary, Changes, and Testing sections; optional sections
(Motivation, Technical Approach, Breaking Changes, Deployment/Migration,
Risks, Reviewer Focus, Related Work) appear only when they're supported by
the diff, never as empty placeholders. It doesn't reproduce the diff, list
changed files, or claim test results that weren't actually observed.

See `SKILL.md` for branch resolution, analysis requirements, and output rules.
