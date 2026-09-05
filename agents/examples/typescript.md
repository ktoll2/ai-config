# Project Instructions

Node/TypeScript project using `npm` (swap in `pnpm`/`yarn` commands if this
project uses one of those instead - check for the matching lockfile).

## Architecture

- `src/` - application/library source, compiled by `tsc`/bundled by the
  project's build tool.
- `src/**/__tests__/` or `*.test.ts` next to the file it tests - check which
  convention the existing tests use before adding a new one.
- Shared types live near what they describe, not in a single catch-all
  `types.ts` once a project grows past a handful of them.

## Commands

```bash
npm install                     # install dependencies

npm run dev                     # local dev server, if applicable
npm run build                   # production build
npm test                        # run the full test suite
npm test -- path/to.test.ts     # run a focused test file
npm run test -- -t "test name"  # run a focused test case (vitest/jest)

npm run lint                    # eslint
npm run format                  # prettier
npx tsc --noEmit                # type check without emitting output
```

## Conventions

- Strict TypeScript: don't add `any` or `// @ts-ignore` to work around a
  type error - fix the type or narrow it.
- Prefer named exports over default exports.
- Async code uses `async`/`await`, not raw `.then()` chains, except where
  the existing code already does otherwise.
- Keep React (or other framework) components small and colocate
  component-specific state/hooks with the component, not in a global store,
  unless the state is genuinely shared.

## Testing

- Use the project's configured runner (`vitest`, `jest`, etc.) - check
  `package.json`'s `test` script rather than assuming.
- Prefer testing behavior through the public API/rendered output over
  implementation details (e.g. Testing Library queries over inspecting
  component internals).
- Mock network calls at the boundary (fetch/axios), not deep inside
  business logic.
