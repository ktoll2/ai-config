# AI Configuration

Portable, tool-neutral instructions and workflows for AI-assisted development.
The content directories are the source of truth. Tool directories contain the
small adapters and machine-specific settings needed to install that content
into a specific AI tool.

## Layout

- `agents/` — self-contained agent instructions by scope or specialty.
- `skills/` — repeatable workflows, one directory per skill. Each skill has a
  `SKILL.md` for the agent workflow and a `README.md` for human-facing usage.
- `rules/` — small, reusable policy documents.
- `commands/` and `prompts/` — tool-neutral command concepts and prompt
  material. Tool adapters provide executable slash-command definitions.
- `profiles/` — future combinations of agents, rules, and skills.
- `templates/` — starting points for project-local configuration.
- `tools/` — tool-specific configuration and installation notes.
- `scripts/` — reserved for future maintenance utilities.

## OpenCode

The current OpenCode setup is represented by:

- `agents/global/AGENTS.md`
- `skills/`
- `tools/opencode/opencode.jsonc`
- `tools/opencode/agents/`
- `tools/opencode/commands/`

## OpenCode Symlinks

Optionally link the OpenCode adapter into your global configuration directory:

```text
~/.config/opencode/
├── AGENTS.md              -> agents/global/AGENTS.md
├── agents/                -> tools/opencode/agents/
├── commands/              -> tools/opencode/commands/
├── opencode.jsonc         -> tools/opencode/opencode.jsonc
└── skills/                -> skills/
```

Before creating links, manually move or remove any existing conflicting files
in `~/.config/opencode/`, including `opencode.json`, to prevent unintended
configuration merging. Set `repo` to this repository's absolute path, then run:

```bash
repo=/absolute/path/to/ai-config
mkdir -p ~/.config/opencode
ln -s "$repo/agents/global/AGENTS.md" ~/.config/opencode/AGENTS.md
ln -s "$repo/tools/opencode/agents" ~/.config/opencode/agents
ln -s "$repo/tools/opencode/commands" ~/.config/opencode/commands
ln -s "$repo/tools/opencode/opencode.jsonc" ~/.config/opencode/opencode.jsonc
ln -s "$repo/skills" ~/.config/opencode/skills
```

Restart OpenCode after changing its configuration; it loads configuration only
at startup.

## Adding Content

Keep reusable content tool-neutral. For example, add a new skill as
`skills/<skill-name>/SKILL.md`, then extend the relevant tool adapter only
when that tool needs special metadata or installation behavior.

For example, `skills/pr-summary/` contains the portable pull-request summary
workflow; `tools/opencode/commands/pr-summary.md` exposes it as
`/pr-summary` in OpenCode.

Do not store credentials, tokens, or machine-specific secrets in this
repository. Use environment-variable references in tool adapters when needed.
