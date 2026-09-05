# Templates

Starting points for project-local configuration - files meant to be copied into a project, not installed globally the way `agents/global/AGENTS.md` or a `tools/<tool>/` adapter is.

## What's here

- [`project/AGENTS.md`](project/AGENTS.md) - a blank project-instructions file: headings for architecture, commands, conventions, and testing guidance, with none of it filled in. Copy it into a project root as `AGENTS.md` and fill in what's specific to that project (check a given tool's `tools/<tool>/README.md` if it expects a different filename). See `agents/examples/` for what a filled-in version looks like for a few common language stacks, and `agents/examples/README.md` for the copy/symlink commands.

## Adding a template

A template belongs here when it's something a project copies in and edits, rather than something installed once per tool or machine (that belongs under `tools/<tool>/` instead). Keep templates minimal and unopinionated about specifics - they should prompt whoever fills them in for the right information, not assume a particular stack (that's what `agents/examples/` is for).
