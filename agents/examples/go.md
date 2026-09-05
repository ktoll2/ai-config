# Project Instructions

Go module using the standard toolchain, no build system beyond `go build`.

## Architecture

- `cmd/<binary>/main.go` - entry points, one directory per binary.
- `internal/` - application code not meant for external import.
- `pkg/` - code intended for use by other modules, if any.
- Package boundaries follow domain concepts, not technical layers; avoid a
  generic `utils` or `common` package.

## Commands

```bash
go build ./...              # build everything
go run ./cmd/<binary>        # run a specific binary
go test ./...                # run all tests
go test ./... -run TestName  # run a focused test
go test ./... -race          # run with the race detector before merging
go vet ./...                 # static analysis
gofmt -l .                   # list files needing formatting
golangci-lint run            # full lint suite (if configured)
```

## Conventions

- Format with `gofmt`/`goimports` before committing; do not hand-format.
- Return errors, don't panic, except for truly unrecoverable startup
  failures. Wrap errors with context using `fmt.Errorf("...: %w", err)`.
- Prefer small interfaces defined at the point of use (consumer-side),
  not alongside the implementation.
- Pass `context.Context` as the first parameter of functions that do I/O or
  can be cancelled; don't store it in a struct.
- Keep exported identifiers documented with a doc comment starting with the
  identifier's name.

## Testing

- Table-driven tests are the default style; use `t.Run` subtests for each
  case.
- Use `testify/require` (or the standard library's `t.Fatalf`) for
  assertions - check what the existing tests use before introducing a new
  assertion library.
- Run `go test ./... -race` for anything touching goroutines or shared
  state before considering it done.
