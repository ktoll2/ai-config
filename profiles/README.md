# Profiles

A profile is a named combination of agents, rules, and skills for a particular kind of work - e.g. "backend development" or "read-only review" - so a tool can be pointed at one concept instead of assembling the pieces by hand each time. This directory is currently empty; it's reserved for when a single agent/rule/skill combination is reused often enough to be worth naming.

## Intended shape

A profile would be a short Markdown file listing what it's made of and why, for example:

```markdown
# Read-Only Review

For an independent review pass with no edit access.

- Agent: `agents/global/AGENTS.md`, Code Review section
- Rules: `rules/git.md`, `rules/coding.md`
- Skills: `skills/code-review/`
- Tool mapping: `tools/claude/agents/reviewer.md`, `tools/opencode/agents/reviewer.md`
```

The profile itself doesn't duplicate the referenced content, only names it - the same "write once, reference everywhere" principle as the rest of this repo. A tool adapter's agent/subagent files (like the `reviewer` subagents already in `tools/claude/agents/` and `tools/opencode/agents/`) are the closest existing thing to a profile today; formalizing `profiles/` would mean defining the combination once, tool-neutrally, and having each adapter's agent file point back at a named profile instead of re-deriving the combination itself.

## Adding a profile

Only add one once a specific combination of agents/rules/skills is actually reused, not speculatively. Name it after the kind of work it supports, list exactly what it's composed of, and update any tool adapter that should reference it.
