# OpenCode Adapter

This adapter installs the tool-neutral global instructions and skills into
OpenCode.

- `opencode.jsonc` retains the pinned parser plugin and global permissions.
- `agents/` contains one file per OpenCode agent. The frontmatter holds
  OpenCode-specific mode, step, and permission settings; the Markdown body is
  the agent prompt. The `reviewer`, `investigator`, and `tester` agents are
  intentionally disabled templates; enable one by removing `disable: true`
  from its frontmatter.
- `commands/` contains OpenCode slash-command adapters for reusable skills.
  `pr-summary.md` runs with OpenCode's read-only `plan` agent and supports
  `/pr-summary`, `/pr-summary <target>`, and explicit `--source` / `--target`
  branch selection.
- Create symlinks from the global OpenCode directory to `agents/global/AGENTS.md`,
  this adapter's `agents/` and `commands/` directories, and `skills/`. The root
  README provides the exact commands.

The adapter contains no credentials; add credentials through environment
variables or a local override, not this repository. Restart OpenCode after
changing configuration.
