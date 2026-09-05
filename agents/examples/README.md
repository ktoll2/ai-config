# Example Project Instructions

`templates/project/AGENTS.md` is the blank starting point for a project-local instructions file. The files in this directory are examples of what a *filled-in* one looks like for a few common language stacks - concrete build/test/lint commands and language-specific conventions, on top of the same structure as the template.

- [`go.md`](go.md) - Go module, standard toolchain
- [`python.md`](python.md) - Python with `pyproject.toml`, `pytest`, `ruff`
- [`typescript.md`](typescript.md) - Node/TypeScript with `npm` and `vitest`
- [`dotnet.md`](dotnet.md) - .NET / C# solution

## Using one

### Copy (recommended)

Copy the closest match into your project root as `AGENTS.md`, then edit the commands, paths, and conventions to match your actual project instead of the illustrative ones here:

```bash
repo=/absolute/path/to/ai-config   # this repository's absolute path
cp "$repo/agents/examples/go.md" ./AGENTS.md
```

Once copied, the file is yours to diverge - editing it has no effect on this repo. Don't leave placeholder commands that don't match your project; an agent that runs an example command against the wrong project wastes a turn finding out it doesn't exist.

Some tools expect a different project-memory filename than `AGENTS.md` - check that tool's `tools/<tool>/README.md` for the name it actually reads, and copy to that filename instead (or in addition).

### Symlink (only if you intend to keep editing the shared copy)

Symlinking keeps the project file and this repo's example in sync, but that also means project-specific edits land back in this shared repo - only do this if that's actually what you want, e.g. while you're still drafting the example itself:

```bash
ln -s "$repo/agents/examples/python.md" ./AGENTS.md
```

For anything you intend to customize per project (the normal case), copy instead of symlinking.

Keep the file focused on what isn't already covered by `agents/global/AGENTS.md` and `rules/`: this repo's global instructions already cover general engineering practice, so a project file should mostly add the project-specific facts an agent can't derive on its own - where things live, which exact commands to run, and any conventions unique to this codebase.
