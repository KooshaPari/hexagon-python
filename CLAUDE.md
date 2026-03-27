# hexagon-python

Hexagonal Architecture (Ports & Adapters) template for Python. Clean, SOLID, DDD-ready scaffold for Python services.

## Stack
- Language: Python 3.12+
- Key deps: uv (package manager), pytest, ruff
- Docs: `docs/`, `adr/`

## Structure
- `domain/`: Pure Python domain layer (entities, value objects, domain services — no framework imports)
- `application/`: Use cases, inbound/outbound port protocols
- `adapters/`: Primary (FastAPI/CLI) and secondary (DB/external) adapters
- `adr/`: Architecture Decision Records

## Key Patterns
- Strict hexagonal layers: domain imports nothing outside stdlib
- Ports as Python `Protocol` types (structural subtyping)
- Dependency injection at composition root
- DDD naming: entities, aggregates, value objects, domain events

## Adding New Functionality
- Domain logic: `domain/`
- Use cases: `application/`
- Adapters: `adapters/primary/` or `adapters/secondary/`
- Use `uv run pytest` to run tests, `uv run ruff check .` to lint
