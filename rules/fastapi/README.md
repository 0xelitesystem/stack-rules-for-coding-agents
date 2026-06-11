# FastAPI rules

## Stack version

- FastAPI 0.110+
- Python 3.11+
- Pydantic 2.x
- SQLAlchemy 2.x (async)
- pytest 8.x

## What this optimizes for

- Strict type safety (FastAPI uses types for validation, OpenAPI generation, IDE support)
- Async-first request handling
- Clean separation between routers, services, and DB models
- Testability via dependency injection

## What this is NOT for

- Sync-only Python codebases (Django, Flask)
- Single-file scripts
- Notebook-style data science code

## Tested in

- Cursor
- Claude Code

## Customize for your team

- Replace SQLAlchemy with your ORM (Tortoise, SQLModel)
- Add framework-specific rules if using `fastapi-users`, `taskiq`, etc.
- Adjust testing rules for your DB setup
