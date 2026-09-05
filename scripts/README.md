# Scripts

Small, documented maintenance utilities for things that can't be handled directly through the repository's configuration files. This directory is currently empty - nothing here has needed a script yet, since installing an adapter today is a handful of `ln -s` commands (documented in each `tools/<tool>/README.md`) rather than something that needs automating.

## What belongs here

- A script that automates a repetitive maintenance task across the repo (e.g. validating that every `skills/*/SKILL.md` has a matching `README.md`, or that every tool adapter's command list matches the skills it exposes).
- An installer that runs a tool adapter's documented symlink steps for the user, if the manual `ln -s` commands in `tools/<tool>/README.md` ever become worth automating.

## What doesn't

- Anything tool-specific enough to belong in `tools/<tool>/` instead.
- One-off, per-machine setup that isn't reusable across checkouts.

## Conventions

- Keep scripts portable (POSIX shell or a widely available interpreter) unless there's a specific reason not to.
- Never modify user configuration (symlinks, settings files, credentials) without explicit confirmation from whoever runs the script.
- Document usage at the top of the script itself, and link to it from the root README so it's discoverable.
