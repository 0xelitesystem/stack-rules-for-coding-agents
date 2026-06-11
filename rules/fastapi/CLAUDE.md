# FastAPI (Python 3.11+)

## Project structure

```
app/
  main.py              # FastAPI app instance, include routers here
  config.py            # Settings from env via pydantic-settings
  dependencies.py      # Reusable Depends() callables (auth, db session)
  routers/             # One file per resource: users.py, orders.py
  models/              # Pydantic models (request/response schemas)
  db/                  # SQLAlchemy models + session factory
  services/            # Business logic, kept out of routers
  tests/               # pytest tests, mirror app/ structure
pyproject.toml
```

Routers are thin: parse input, call a service, return output. Business logic in services.

## Type hints are mandatory

- All function signatures have type hints. No `def foo(x):`, write `def foo(x: int) -> str:`
- Use `from __future__ import annotations` at the top of every module
- Modern syntax: `list[str]` not `List[str]`, `dict[str, int]` not `Dict[str, int]`
- Use `X | None` not `Optional[X]`

## Pydantic for schemas, SQLAlchemy for DB

- Pydantic v2 syntax (`model_validate`, `model_dump`, `Field`)
- DB models and request/response schemas are SEPARATE classes. Don't expose ORM models directly.
- Use `model_config = ConfigDict(from_attributes=True)` on response schemas to read from ORM objects.

## Async by default

- Routers are `async def`
- DB calls use the async session (SQLAlchemy 2.x async, or asyncpg directly)
- Don't mix sync and async DB calls in the same request
- Pure CPU work doesn't need async; use `def` for those handlers

## Dependency injection

- Auth, DB sessions, current user: all via `Depends()`
- Define reusable dependencies in `app/dependencies.py`
- Don't call services directly from routers, inject them too if they need state

## Error handling

- Raise `HTTPException(status_code=404, detail="...")` for client errors
- Don't return `{"error": ...}` from routers manually
- Use a single global exception handler for unexpected errors (returns 500 + log id)
- Validation errors are handled by FastAPI automatically; trust it

## Testing

- pytest with `pytest-asyncio`
- Use `TestClient` (sync) or `AsyncClient` from httpx (async)
- Override dependencies with `app.dependency_overrides` instead of patching
- Each test gets a fresh DB transaction that rolls back at the end

## Don't do this

- Don't put SQL queries inside routers
- Don't use `print()` for logging, use the `logging` module
- Don't catch `Exception` broadly inside routers
- Don't use `eval` or `exec` (also: never)
- Don't disable Pydantic validation to "make it work"
- Don't return database model instances from routers (always go through a Pydantic response model)
