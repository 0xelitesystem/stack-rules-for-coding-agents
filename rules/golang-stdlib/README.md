# Go (stdlib) rules

## Stack version

- Go 1.22+ (uses `http.ServeMux` patterns introduced then)
- Standard library + minimal third-party dependencies
- Tested with the Go toolchain (`go test`, `go vet`, `staticcheck`)

## What this optimizes for

- Long-term maintainability (stdlib doesn't churn like third-party libs)
- Predictability (no framework magic)
- Small, focused dependencies
- Idiomatic error handling and concurrency

## What this is NOT for

- Go projects that have already adopted a heavy framework (Gin, Echo, Fiber, Buffalo)
- Microservice meshes that need framework-level support for tracing/discovery
- Generated code (gRPC, OpenAPI codegen)

## Tested in

- Cursor
- Claude Code

## Customize for your team

- If using `chi`: replace the `net/http` rules with `chi` patterns
- If using `sqlx` or `pgx` directly: adjust the DB rules
- If using a structured logging library other than `slog`: swap that in
