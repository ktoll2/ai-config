# Tool Adapters

Each subdirectory here is a tool-specific adapter: the small amount of frontmatter, config, and permission syntax a specific AI coding tool needs on top of the shared, tool-neutral content in `agents/`, `skills/`, and `rules/`. An adapter should contain no reusable content of its own, only the translation of that content into a given tool's native format, plus that tool's own facts (exact filenames, config keys, invocation syntax) - which belong here and only here, not restated in the generic directories.

## Current adapters

| Tool | Directory |
|---|---|
| Claude Code | [`claude/`](claude/) (see [`claude/README.md`](claude/README.md)) |
| OpenCode | [`opencode/`](opencode/) (see [`opencode/README.md`](opencode/README.md)) |

## Adding a new adapter

Work through each generic concept and figure out that tool's equivalent. Not every tool will have one for everything below; when it doesn't, say so in the new adapter's README rather than forcing a fit.

1. **Global instructions.** Every adapter so far installs `agents/global/AGENTS.md` as the tool's default system/memory prompt, usually by symlinking it directly since the content is already plain Markdown. Figure out that tool's global memory file (and its exact path/filename) and document the symlink in the new adapter's README.
2. **Skills.** `skills/<name>/SKILL.md` already uses a `name`/`description` frontmatter that more than one tool reads natively. Check whether the new tool can load `skills/` as-is (a directory symlink, no translation) before writing any per-skill adapter file - both existing adapters do this and need nothing else for a skill to be usable.
3. **Rules.** `rules/*.md` are policy text, not enforcement. Find the tool's actual enforcement mechanism (a permissions/settings file, an agent's tool allow-list, a project config block) and translate each rule into it. Document the mapping in that tool's own README; `rules/README.md`'s table only needs a short, generic pointer back to it (see the `git.md` row there for the pattern), not the specifics themselves.
4. **Commands.** A skill that should also be reachable as an explicit slash command gets one file per command under `tools/<tool>/commands/`, using that tool's frontmatter, with a body that just says to use the skill (see `tools/claude/commands/pr-summary.md` and `tools/opencode/commands/pr-summary.md`). Keep the actual behavior defined once, in the skill or in `commands/<name>.md`; the adapter file should be a thin pointer, not a restatement.
5. **Agents/subagents.** Map specialized workflows (`investigator`, `reviewer`, `tester`, etc.) to the tool's agent/subagent concept, restricting each one's tool access to match its purpose. Tools differ here more than anywhere else - don't assume feature parity:
   - If the tool supports disabling an agent in its own frontmatter (like OpenCode's `disable: true`), ship it disabled by default and document how to enable it.
   - If it doesn't (like Claude Code, where a subagent is live as soon as its file exists in the agents directory), don't fake the missing feature - instead keep the agent file out of the tool's live config directory by default, and document the opt-in symlink per agent.
   - If the tool has no per-agent, per-command permission filtering (most don't), don't try to reproduce a fine-grained allow/ask/deny table in the agent file - restrict by tool access instead (no `Bash`, no `Edit`, etc.) and say plainly what capability that trades away (e.g. a read-only agent without `Bash` can't run `git diff` itself).
6. **README structure.** Mirror the shape of `tools/claude/README.md` / `tools/opencode/README.md`: a short intro, "What's in this directory" with a tree and a table per piece, "Install" with copy-pasteable commands, an "Enabling a subagent/agent" section if applicable, "Using the slash command(s)" with example invocations, and "Keeping this in sync" pointing back at the generic directories.
7. **Root README.** Add a row to the "Supported Tools" table in the root `README.md` linking to the new adapter's README. Don't add tool-specific detail to the root README itself - it stays an index.

## Keeping adapters and generic content honest

- A generic directory (`agents/`, `skills/`, `rules/`, `mcp/`, `profiles/`, `prompts/`, `commands/`, `templates/`, `scripts/`) should describe *concepts*, and point to `tools/<tool>/README.md` for how a specific tool implements one - it should not itself assert a tool's exact filename, config key, or behavior. If you find yourself naming a specific tool's file or field outside `tools/<tool>/`, move that fact into the adapter and leave a generic pointer behind instead.
- If two adapters need to state the same fact about how they're built (not about a specific tool), put it here instead of duplicating it in both READMEs.
- When a tool changes its config format or adds a feature relevant to an existing mapping above (e.g. gains per-agent command permission filtering), update that tool's adapter and re-check whether the workaround documented for its old limitation is still needed.
