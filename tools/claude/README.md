# Claude Code Adapter

This directory adapts the tool-neutral content in this repo - global instructions, skills, subagents, and slash commands - into the file formats Claude Code actually reads. Nothing here is Claude-specific *content*; it's the small amount of frontmatter and permission syntax Claude Code needs on top of the shared material in `agents/`, `skills/`, and `rules/`.

If you just want to get set up, skip to [Install](#install).

## What's in this directory

```text
tools/claude/
├── README.md          this file
├── settings.json       session-wide permission rules (snippet to merge)
├── agents/              subagent definitions (disabled by default)
│   ├── investigator.md
│   ├── reviewer.md
│   └── tester.md
└── commands/            slash-command definitions
    └── pr-summary.md
```

### `settings.json` - permission rules

Claude Code checks a `permissions` block in `settings.json` before running a tool. This file's `permissions.allow` / `.ask` / `.deny` arrays encode the policy in `rules/git.md` as Claude Code permission rules: read-only Git/inspection commands are allowed, likely-sensitive files (`.env`, `*.pem`, anything with "secret"/"token"/"credential" in the name) prompt before reading, and destructive Git or shell commands (`git push`, `git reset`, `rm -rf`, `sudo`, ...) are denied outright.

This file is a **snippet to merge**, not something to symlink in as-is - you already have (or will have) other settings in `~/.claude/settings.json`, and overwriting it would lose them. See [Install](#install) for how to merge it.

### `agents/` - subagents (disabled by default)

Each file is a Claude Code subagent: a specialist Claude can delegate to for a specific kind of task, with its own system prompt and its own restricted tool list.

| Agent | Tools it gets | What it's for |
|---|---|---|
| `investigator` | `Read`, `Grep`, `Glob` | Diagnoses bugs and unfamiliar code by reading, without touching anything. No `Bash`, so it can't run `git diff`/`git log` - it works from current file contents. |
| `reviewer` | `Read`, `Grep`, `Glob` | Independent code review, same read-only restriction as `investigator`. |
| `tester` | `Read`, `Grep`, `Glob`, `Bash` | Runs the test suite and triages failures. Keeps `Bash` (it has to, to run tests) but has no `Edit`/`Write`, so it can't touch source. |

Claude Code has no per-agent "disabled" flag - a subagent is live the moment its file exists under `~/.claude/agents/`. So instead, **the install instructions leave `~/.claude/agents/` empty by default**, and you opt in to each subagent one at a time by symlinking its file in. See [Enabling a subagent](#enabling-a-subagent).

There's no subagent for general-purpose implementation work, because Claude Code doesn't need one for that: the main Claude Code loop already reads `CLAUDE.md` and `settings.json` directly, which the rest of this adapter covers.

### `commands/` - slash commands

| Command | Backed by | Notes |
|---|---|---|
| `/pr-summary` | `skills/pr-summary/SKILL.md` | Generates a reviewer-focused PR summary from a branch comparison. `allowed-tools` restricts it to `Read`/`Grep`/`Glob` plus read-only `git` inspection - it can't edit files or touch history. |

## Install

Symlinking keeps everything pointing at this repo, so future edits here show up in Claude Code without reinstalling anything.

```bash
repo=/absolute/path/to/ai-config   # this repository's absolute path

# Global instructions -> Claude Code's global memory file
ln -s "$repo/agents/global/AGENTS.md" ~/.claude/CLAUDE.md

# Skills load as-is; Claude Code's SKILL.md format is what's already here
ln -s "$repo/skills" ~/.claude/skills

# Slash commands
ln -s "$repo/tools/claude/commands" ~/.claude/commands

# Subagents: create a real (non-symlinked) directory, empty by default
mkdir -p ~/.claude/agents
```

Before running these, move or remove anything already at `~/.claude/CLAUDE.md`, `~/.claude/skills`, or `~/.claude/commands` - symlinking on top of an existing file/directory will fail, and merging a real directory with a symlinked one silently hides one or the other.

Then merge the permission rules:

```bash
cat "$repo/tools/claude/settings.json"
```

Copy the `permissions` object into `~/.claude/settings.json` by hand (or merge it with `jq`, see [Updating settings.json](#updating-settingsjson)). If `~/.claude/settings.json` doesn't exist yet, you can just copy the whole file:

```bash
mkdir -p ~/.claude
cp "$repo/tools/claude/settings.json" ~/.claude/settings.json
```

Restart Claude Code - it only reads `CLAUDE.md`, `settings.json`, `agents/`, `commands/`, and `skills/` at startup.

### Project-level instructions

At the project level (as opposed to the global `~/.claude/` install above), Claude Code reads `CLAUDE.md` at the project root, falling back to `AGENTS.md` if `CLAUDE.md` isn't present. `templates/project/AGENTS.md` and `agents/examples/` are written as `AGENTS.md` by convention; copy one to `CLAUDE.md` instead (or in addition) if you want Claude Code to prefer it over a project's existing `AGENTS.md`.

### Enabling a subagent

Each subagent in `tools/claude/agents/` is inert until it's linked into `~/.claude/agents/`. Enable the ones you want:

```bash
ln -s "$repo/tools/claude/agents/investigator.md" ~/.claude/agents/investigator.md
ln -s "$repo/tools/claude/agents/reviewer.md" ~/.claude/agents/reviewer.md
ln -s "$repo/tools/claude/agents/tester.md" ~/.claude/agents/tester.md
```

Run only the lines for the agents you actually want available - that's the whole mechanism for "disabling" one. To disable an agent later, remove its symlink:

```bash
rm ~/.claude/agents/tester.md
```

Once enabled, Claude Code can delegate to a subagent on its own when the task matches its `description`, or you can call it out explicitly in a prompt, e.g.:

```text
> use the reviewer agent to look over this diff
> have the investigator agent figure out why this test is flaky
```

### Updating `settings.json`

If you'd rather merge programmatically than by hand, and you have `jq` installed:

```bash
jq -s '.[0] * .[1]' ~/.claude/settings.json "$repo/tools/claude/settings.json" \
  > /tmp/claude-settings.json \
  && mv /tmp/claude-settings.json ~/.claude/settings.json
```

`*` is `jq`'s recursive merge - it merges the `permissions.allow` / `.ask` / `.deny` arrays' *parent object*, but arrays themselves are replaced, not concatenated. If you already have your own `permissions.allow` entries, diff the two files and combine the arrays by hand instead of merging blindly:

```bash
diff <(jq .permissions ~/.claude/settings.json) \
     <(jq .permissions "$repo/tools/claude/settings.json")
```

## Using the slash command

```text
> /pr-summary
> /pr-summary main
> /pr-summary --source feature/checkout --target release/2.4
```

With no arguments it summarizes the current branch against the repository's detected default branch; see `skills/pr-summary/SKILL.md` for the full branch-resolution and output rules.

## Keeping this in sync

Everything reusable lives outside `tools/claude/` - in `agents/`, `skills/`, and `rules/`. When you add a new skill, it's available to Claude Code for free via the `skills/` symlink; only add a file here if the skill also needs a slash command (see `tools/claude/commands/pr-summary.md` for the pattern) or a dedicated subagent (see `tools/claude/agents/` for the pattern). Don't put credentials, tokens, or machine-specific secrets in this directory - use environment variables or a local, untracked override instead.
