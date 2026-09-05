# Project Instructions

.NET solution (`.sln`) with one or more C# projects, built with the `dotnet`
CLI.

## Architecture

- `src/<Project>/` - one directory per project referenced by the solution.
- `tests/<Project>.Tests/` - mirrors `src/`, one test project per source
  project.
- Cross-cutting concerns (logging, configuration) are injected via
  constructor dependency injection, not accessed through static state.

## Commands

```bash
dotnet restore                          # restore NuGet packages
dotnet build                            # build the whole solution
dotnet build src/<Project>              # build a single project

dotnet test                             # run all tests
dotnet test tests/<Project>.Tests       # run one test project
dotnet test --filter "FullyQualifiedName~TestName"   # run a focused test

dotnet format                           # apply code style rules
dotnet format --verify-no-changes       # check formatting in CI
```

## Conventions

- Nullable reference types are enabled; don't suppress warnings with `!`
  unless nullability has actually been checked immediately before.
- Use `async`/`await` all the way up the call stack for I/O-bound work; avoid
  `.Result`/`.Wait()`, which can deadlock.
- Prefer records for immutable data transfer objects.
- Follow standard .NET naming: `PascalCase` for types/methods/properties,
  `camelCase` for locals/parameters, `_camelCase` for private fields.
- Public APIs get XML doc comments (`///`) on new or changed members.

## Testing

- Use the project's existing framework (xUnit, NUnit, or MSTest - check an
  existing test file rather than assuming xUnit).
- Prefer `Theory`/`InlineData` (xUnit) or the equivalent parameterized-test
  feature over copy-pasted near-identical test methods.
- Keep unit tests isolated from real databases/network/filesystem; use the
  project's existing fakes or an in-memory provider.
