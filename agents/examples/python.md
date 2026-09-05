# Project Instructions

Python project managed with `pyproject.toml`, dependencies installed into a
virtual environment (adjust the exact package manager - `pip`, `poetry`, or
`uv` - to match this project).

## Architecture

- `src/<package>/` - application/library code (src layout, not a top-level
  package next to `pyproject.toml`).
- `tests/` - mirrors the `src/<package>/` structure, one test module per
  source module.
- Configuration and environment-specific values come from environment
  variables or a settings module, never hardcoded.

## Commands

```bash
python -m venv .venv && source .venv/bin/activate   # first-time setup
pip install -e ".[dev]"                              # install with dev deps

pytest                          # run the full test suite
pytest tests/path/test_x.py -k test_name   # run a focused test
pytest --cov=src                # run with coverage

ruff check .                    # lint
ruff format .                   # format
mypy src                        # type check
```

## Conventions

- Type hints are required on new/changed function signatures; run `mypy`
  before considering a change done.
- Format and lint with `ruff` (or `black`/`flake8` if that's what the
  project already uses) - check `pyproject.toml` for the actual configured
  tools before assuming.
- Prefer `pathlib.Path` over `os.path` string manipulation.
- Use dataclasses or `pydantic` models for structured data, not bare dicts,
  once a shape is used in more than one place.
- Avoid bare `except:`; catch specific exceptions and re-raise with context
  (`raise NewError(...) from err`) when translating exception types.

## Testing

- Use `pytest` fixtures for setup/teardown, not `setUp`/`tearDown` methods,
  unless the codebase already uses `unittest`.
- Keep tests deterministic: mock time, randomness, and network calls at the
  boundary rather than relying on real ones.
- For a bug fix, add a regression test that fails on the old code and
  passes on the fix.
