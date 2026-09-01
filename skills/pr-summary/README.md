# Pull Request Summary Skill

Produces concise, reviewer-focused pull request summaries from a read-only
`target...source` Git comparison.

The OpenCode adapter exposes this skill through `/pr-summary`. It supports the
current branch into the detected default target, an explicit target positional
argument, or explicit `--source` and `--target` arguments.

See `SKILL.md` for branch resolution, analysis requirements, and output rules.
