# Prompts

Reusable prompt material that's smaller than a full skill: fragments, phrasing, or a single reusable instruction block that more than one skill, agent, or ad hoc session might want, organized by purpose rather than by tool. This directory is currently empty.

## Prompts vs. skills vs. rules

- **`rules/`** is policy ("do X, don't do Y").
- **`skills/<name>/SKILL.md`** is a full, triggerable workflow built out of policy plus steps.
- **`prompts/`** is neither a policy nor a complete workflow - it's reusable *wording*: a phrasing for asking an agent to summarize something a particular way, a reusable few-shot example, a snippet two or more skills would otherwise duplicate.

If a piece of prompt text is only ever used in one place, write it inline where it's used instead of extracting it here - this directory is for material that's actually shared.

## Adding prompt material

Organize by purpose, e.g. `prompts/summarization/concise.md` or `prompts/review/severity-ordering.md`, not by which tool or skill happens to use it first. Reference a prompt file from the skill or agent instructions that use it rather than copying its text in, so an edit here doesn't need to be repeated at each call site.
