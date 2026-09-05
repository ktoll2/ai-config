# Agents

Self-contained agent instructions, by scope or specialty.

- [`global/AGENTS.md`](global/AGENTS.md) - the one global instruction file every tool adapter installs as that tool's default system/memory prompt. It covers general engineering practice: investigation before changes, implementation conventions, testing and verification, code review, security, and Git restrictions. See that tool's `tools/<tool>/README.md` for exactly where and how it gets installed.
- [`examples/`](examples/) - filled-in examples of a *project-level* instructions file (Go, Python, TypeScript, .NET), showing what `templates/project/AGENTS.md`'s blank starting point looks like once filled in with real commands and conventions for a stack. See `agents/examples/README.md` for how to copy one into a project.

## Global vs. project-level vs. examples

- `global/AGENTS.md` applies everywhere, for every project, regardless of language or stack - it's installed once per tool, not per project.
- `templates/project/AGENTS.md` is the blank per-project file a project copies in and fills out with what's specific to it.
- `examples/` shows what that filled-out file tends to look like for a few common stacks, as a starting point to copy and edit rather than write from scratch.

A project-level file should only add what `global/AGENTS.md` and `rules/` don't already cover - where things live, exactly which commands to run, and conventions unique to that codebase.
