# AI Configuration

Portable, tool-neutral instructions and workflows for AI-assisted development. The content directories are the source of truth: agent instructions, rules, and skills written once and shared across whatever AI coding tool you use. Tool directories contain only the small adapters and machine-specific settings needed to install that content into a specific tool.

The goal is to avoid maintaining the same coding conventions, review checklist, or bug-investigation workflow N times, once per tool, drifting further apart each time something changes. Write it once here; each tool adapter is a thin translation layer, not a second copy.

## Layout

```text
ai-config/
├── agents/       self-contained agent instructions, by scope or specialty
│   ├── global/     the one global instruction file every adapter installs
│   └── examples/   filled-in project AGENTS.md examples, by language
├── skills/       repeatable workflows, one directory per skill
├── rules/        small, reusable policy documents (git, testing, coding)
├── commands/     tool-neutral command concepts
├── prompts/      reusable prompt material
├── profiles/     future combinations of agents, rules, and skills
├── templates/    starting points for project-local configuration
├── tools/        tool-specific adapters (see Supported Tools below,
│                 and tools/README.md for the adapter pattern itself)
└── scripts/      reserved for future maintenance utilities
```

Every top-level directory has its own `README.md` with more detail than the one-liners above, including the currently-empty ones (`commands/`, `mcp/`, `profiles/`, `prompts/`, `scripts/`), which explain what belongs there and what doesn't.

- `agents/global/AGENTS.md` is the one global instruction file every tool adapter installs as that tool's default system/memory prompt. `agents/examples/` shows what a filled-in *project-level* instructions file looks like for a few common language stacks - see `templates/project/AGENTS.md` for the blank starting point they're based on.
- `skills/<name>/` pairs a `SKILL.md` (the agent-facing workflow) with a `README.md` (human-facing usage notes). The `SKILL.md` format is already native to more than one tool, so most tool adapters load `skills/` directly with no translation at all.
- `rules/` documents are the source policy text (e.g. "Git is inspection-only") that tool adapters translate into that tool's actual enforcement mechanism - a permission block, an agent's tool allow-list, whatever the tool supports.

## Supported Tools

| Tool | Adapter | Install docs |
|---|---|---|
| Claude Code | [`tools/claude/`](tools/claude/) | [`tools/claude/README.md`](tools/claude/README.md) |
| OpenCode | [`tools/opencode/`](tools/opencode/) | [`tools/opencode/README.md`](tools/opencode/README.md) |

Each adapter README covers what's in the directory, step-by-step install commands (mostly symlinks into that tool's global config directory), how to enable or disable its optional agents, and example commands for its slash commands. Start there for whichever tool you use. Adding support for a new tool? See [`tools/README.md`](tools/README.md) for the adapter pattern to follow.

## Adding Content

Keep reusable content tool-neutral. For example, add a new skill as `skills/<skill-name>/SKILL.md`, then extend a tool adapter only when that tool needs special metadata or installation behavior on top of it - a new rule or global-instruction change usually needs no adapter changes at all.

For example, `skills/pr-summary/` contains the portable pull-request summary workflow; `tools/opencode/commands/pr-summary.md` and `tools/claude/commands/pr-summary.md` each expose it as `/pr-summary` in their respective tool. A new skill needs no tool-specific adapter at all unless it also needs a slash command or a dedicated agent - both tools load `skills/` directly.

When adding a new tool adapter, follow [`tools/README.md`](tools/README.md) and add a row to the [Supported Tools](#supported-tools) table above. Keep tool-specific facts (exact filenames, config keys, invocation syntax) inside that tool's own `tools/<tool>/README.md` rather than restating them in a generic directory's README - the generic docs should describe concepts and point to the adapter, not duplicate its specifics.

Do not store credentials, tokens, or machine-specific secrets in this repository. Use environment-variable references in tool adapters when needed.

## Conventions

- Prose paragraphs are written as single lines; let the Markdown renderer wrap them rather than hand-wrapping at a fixed column.
- Don't use em dashes; use a comma, colon, parentheses, or a plain hyphen instead.
- Every directory, including an empty one, gets a `README.md` explaining what belongs there and what doesn't - see any of `commands/`, `mcp/`, `profiles/`, `prompts/`, or `scripts/` for the pattern.
