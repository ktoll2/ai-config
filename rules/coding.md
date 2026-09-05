# Coding Rules

- Follow the existing project's patterns and conventions.
- Prefer focused changes and existing utilities over broad rewrites or new
  abstractions.
- Do not introduce a new abstraction, dependency, or pattern unless it has
  clear value over what already exists.
- Use explicit, strongly typed variables where practical.
- Consider error handling, edge cases, concurrency, and failure paths, not
  just the common case.
- Comment complex or non-obvious logic concisely; do not comment what the
  code already makes obvious.
- Avoid speculative generalization: build for the requirement in front of
  you, not a hypothetical future one.
- Keep functions, files, and modules focused on one responsibility rather
  than accumulating unrelated behavior.
- Remove dead code and commented-out code instead of leaving it in place.
- Preserve public APIs and data formats unless a change is explicitly required.
