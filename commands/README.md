# Commands

Tool-neutral command concepts: the description of what a slash command should do, kept independent of any tool's slash-command file format. This directory is currently empty because the one command this repo defines, `/pr-summary`, is substantial enough to be a full skill instead (see [Commands vs. skills](#commands-vs-skills) below); it lives at `skills/pr-summary/SKILL.md`, and each tool adapter's `tools/<tool>/commands/pr-summary.md` exposes it as `/pr-summary`.

## Commands vs. skills

Both end up as a slash command in a tool, but they differ in how they're reached and how much workflow they carry:

- **`skills/<name>/SKILL.md`** carries its own trigger description, so a tool can invoke it automatically when a task matches, in addition to an explicit command. Use this for anything with a real multi-step workflow (see `skills/pr-summary/SKILL.md`'s branch-resolution and output rules for an example) or that should be discoverable without the user knowing its exact command name.
- **`commands/<name>.md`** (this directory) is for a short, purely explicit prompt: something a user runs by name on purpose, with no auto-invocation and little workflow beyond "do this one thing." It's a plain Markdown file describing the command's behavior and expected arguments, with no tool-specific frontmatter.

## Adding a command

1. Write the tool-neutral behavior here as `commands/<name>.md`: what the command does, how it interprets arguments, and any output format it must produce.
2. For each tool that should expose it, add `tools/<tool>/commands/<name>.md` with that tool's frontmatter (see `tools/claude/commands/pr-summary.md` and `tools/opencode/commands/pr-summary.md` for the pattern), pointing back at this file's behavior.
3. If the command grows a real workflow, trigger conditions, or reusable structure, consider promoting it to a skill under `skills/` instead.
