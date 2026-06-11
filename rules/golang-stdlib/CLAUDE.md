# Go (standard library, minimal dependencies)

## Project structure

```
cmd/
  myservice/
    main.go            # Entry point. Wire dependencies, start server, handle signals.
internal/              # Application code. NOT importable from outside this module.
  config/              # Loading config from env
  http/                # HTTP handlers, middleware
  store/               # DB access (use `database/sql` or sqlc, not an ORM)
  domain/              # Business types and logic
pkg/                   # Genuinely reusable code (rare). Most code goes in internal/
go.mod
go.sum
Makefile               # Common tasks: build, test, lint, run
```

`internal/` is the default. `pkg/` is for code other modules will import, most projects have none.

## Standard library first

- HTTP: `net/http` with `http.ServeMux` (Go 1.22+) or `chi` if you need patterns it doesn't support
- DB: `database/sql` + driver, or `sqlc` for type-safe queries. Avoid GORM unless the team already uses it.
- JSON: `encoding/json`
- Tests: `testing` package; use `testify` only if needed
- Logging: `log/slog` (structured, in stdlib since 1.21)

## Errors

- Wrap with context: `fmt.Errorf("loading config: %w", err)`
- Check errors immediately. Never swallow with `_`.
- Return errors up the stack; only handle (log, retry, default) at the boundary
- Use `errors.Is` and `errors.As` for type checks, not string matching
- Sentinel errors for known cases: `var ErrNotFound = errors.New("not found")`

## Naming

- Package names: short, lowercase, no underscores (`store` not `storage_layer`)
- Acronyms: all uppercase if they're acronyms (`URL`, `ID`, `HTTP`), `userID` not `userId`, `getURL` not `getUrl`
- Receivers: 1-2 letter, consistent across methods (`func (u *User) ...` everywhere, not `(user *User)` sometimes and `(u *User)` other times)
- Interfaces: name by what they DO (`Reader`, `Closer`), not `IThing` or `ThingInterface`

## Concurrency

- Goroutines need a clear lifecycle. Always know how each goroutine exits.
- Pass `context.Context` as the FIRST argument of any function that does I/O
- Never start a goroutine without a way to stop it (context cancellation, channel close, sync.WaitGroup)
- Channels for ownership transfer; mutexes for shared state. Don't use channels just because they're "the Go way."

## Tests

- Test files: `foo_test.go` next to `foo.go`
- Test functions: `TestX`, with subtests via `t.Run("case", ...)` for table-driven tests
- Table-driven tests for any function with multiple cases. Tables go in slices of structs.
- Use `t.Helper()` in test helpers so failures point to the call site
- No mocks for things you can run for real (use a real Postgres in tests via testcontainers)

## Don't do this

- Don't use `init()` functions (hidden side effects)
- Don't use global mutable state
- Don't use `panic` for control flow (only for unrecoverable startup errors)
- Don't use `interface{}` (now `any`) when a concrete type would do
- Don't use generics gratuitously, they have a real cognitive cost
- Don't import third-party packages "to make it nicer" if stdlib works
