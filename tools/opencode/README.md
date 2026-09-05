# OpenCode Adapter

This directory adapts the tool-neutral content in this repo - global instructions, skills, agents, and slash commands - into the file formats OpenCode actually reads. Nothing here is OpenCode-specific *content*; it's the small amount of frontmatter and permission syntax OpenCode needs on top of the shared material in `agents/`, `skills/`, and `rules/`.

If you just want to get set up, skip to [Install](#install).

## What's in this directory

```text
tools/opencode/
├── README.md          this file
├── opencode.jsonc      global OpenCode config (permissions, plugins)
├── agents/              agent definitions
│   ├── build.md          primary agent
│   ├── investigator.md   subagent, disabled by default
│   ├── reviewer.md       subagent, disabled by default
│   └── tester.md         subagent, disabled by default
└── commands/            slash-command definitions
    └── pr-summary.md
```

### `opencode.jsonc` - global config

This is OpenCode's single top-level config file: the pinned parser plugin, `default_agent`, and a `permission` block. The `permission` block is the OpenCode translation of `rules/git.md`: read-only Git/inspection commands (`git status`, `git diff`, `git log`, ...) are allowed, likely-sensitive files (`.env`, `*.pem`, anything with "secret"/"token"/"credential" in the name) prompt before reading, and destructive commands (`sudo *`, `rm -rf *`, and `git *` in general, since only the read-only subcommands above are carved back out) are denied.

Unlike Claude Code's `settings.json`, this file is meant to be symlinked in wholesale - OpenCode doesn't layer a home-directory config on top of a project one the way some other tools do, so there's nothing to merge.

### `agents/` - agents

| Agent | Mode | Tools/permissions | What it's for |
|---|---|---|---|
| `build` | `primary` | Full edit + Git-inspection-only Bash | The main agent you work with day to day. Implements changes, builds, and tests; anything not covered by the read-only Git allowlist prompts for approval. |
| `investigator` | `all`, disabled by default | `Read`/`Grep`/`Glob` + Git-inspection-only Bash, no edit | Diagnoses bugs and unfamiliar code from evidence, including Git history, without changing anything. |
| `reviewer` | `all`, disabled by default | Same read-only shape as `investigator`, plus `task`/`webfetch`/`websearch` explicitly denied | Independent code review, findings ordered by severity, no edits. |
| `tester` | `subagent`, disabled by default | `Read`/`Grep`/`Glob` + only `dotnet test`/`dotnet build`/`npm test`/`npm run test`, no edit | Runs the test suite and triages failures without touching production code. |

`investigator`, `reviewer`, and `tester` ship with `disable: true` in their frontmatter, so they're inert until you remove that line - see [Enabling an agent](#enabling-an-agent).

### `commands/` - slash commands

| Command | Backed by | Notes |
|---|---|---|
| `/pr-summary` | `skills/pr-summary/SKILL.md` | Generates a reviewer-focused PR summary from a branch comparison. Runs under the built-in read-only `plan` agent, so it can't edit files. |

## Install

Symlinking keeps everything pointing at this repo, so future edits here show up in OpenCode without reinstalling anything.

```bash
repo=/absolute/path/to/ai-config   # this repository's absolute path

mkdir -p ~/.config/opencode
ln -s "$repo/agents/global/AGENTS.md" ~/.config/opencode/AGENTS.md
ln -s "$repo/tools/opencode/agents" ~/.config/opencode/agents
ln -s "$repo/tools/opencode/commands" ~/.config/opencode/commands
ln -s "$repo/tools/opencode/opencode.jsonc" ~/.config/opencode/opencode.jsonc
ln -s "$repo/skills" ~/.config/opencode/skills
```

Before running these, move or remove anything already at `~/.config/opencode/AGENTS.md`, `~/.config/opencode/opencode.jsonc` (and any sibling `opencode.json`), `~/.config/opencode/agents`, `~/.config/opencode/commands`, or `~/.config/opencode/skills` - symlinking on top of an existing file/directory will fail, and having both an `opencode.json` and `opencode.jsonc` present can cause unintended configuration merging.

Restart OpenCode - it only reads its configuration at startup.

### Enabling an agent

`investigator`, `reviewer`, and `tester` are disabled out of the box. To turn one on, delete the `disable: true` line from its frontmatter, e.g. in `tools/opencode/agents/reviewer.md`:

```diff
 mode: all
-disable: true
 steps: 10
```

Once enabled:

- **`reviewer` and `investigator`** (`mode: all`) can be reached with an explicit `@` mention in your prompt:

  ```text
  > @reviewer look over this diff
  > @investigator figure out why this test is flaky
  ```

- **`tester`** (`mode: subagent`) isn't directly addressable - `build` (or another primary agent) delegates to it automatically when a task matches its description.

`build` itself (`mode: primary`) is always active; it's the agent OpenCode starts in, and you can cycle between primary agents with **Tab** (or your configured `switch_agent` keybind) if you add more.

To disable an agent again later, put `disable: true` back.

## Using the slash command

```text
> /pr-summary
> /pr-summary main
> /pr-summary --source feature/checkout --target release/2.4
```

With no arguments it summarizes the current branch against the repository's detected default branch; see `skills/pr-summary/SKILL.md` for the full branch-resolution and output rules.

## Keeping this in sync

Everything reusable lives outside `tools/opencode/` - in `agents/`, `skills/`, and `rules/`. When you add a new skill, it's available to OpenCode for free via the `skills/` symlink; only add a file here if the skill also needs a slash command (see `tools/opencode/commands/pr-summary.md` for the pattern) or a dedicated agent (see `tools/opencode/agents/` for the pattern). Don't put credentials, tokens, or machine-specific secrets in this directory - use environment variables or a local, untracked override instead.
