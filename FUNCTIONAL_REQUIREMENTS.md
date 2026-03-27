# Functional Requirements — hexagon-python

## FR-STRUCT-001
The repository SHALL contain a `pyproject.toml` with `[build-system]`, `[project]`, and `[tool.ruff]` sections.

## FR-STRUCT-002
The Python package SHALL be organised as sub-packages: `domain/`, `application/`, `ports/`, `adapters/`.

## FR-STRUCT-003
`domain/` SHALL NOT import from `application/`, `ports/`, or `adapters/`.

## FR-STRUCT-004
`application/` SHALL import only from `domain/` and `ports/`.

## FR-STRUCT-005
`adapters/` SHALL implement protocols or ABCs defined in `ports/`.

## FR-DOMAIN-001
Domain entities SHALL be `@dataclass` or `pydantic.BaseModel` types.

## FR-DOMAIN-002
Domain errors SHALL inherit from a project-defined `DomainError(Exception)` base class.

## FR-DOMAIN-003
Domain package SHALL declare zero third-party imports except optionally `pydantic`.

## FR-PORTS-001
Inbound port interfaces SHALL be defined as `typing.Protocol` or `abc.ABC` in `ports/inbound/`.

## FR-PORTS-002
Outbound port interfaces SHALL be defined in `ports/outbound/`.

## FR-PORTS-003
Async port methods SHALL use `async def` with return type annotations.

## FR-APP-001
Use case `__init__` SHALL accept port instances typed as the protocol/ABC, not concrete adapters.

## FR-APP-002
Use cases SHALL return typed results — never `Any` or bare `dict`.

## FR-ADAPTER-001
At least one in-memory implementation of the outbound port SHALL exist in `adapters/outbound/`.

## FR-ADAPTER-002
At least one inbound adapter stub SHALL exist in `adapters/inbound/`.

## FR-TEST-001
`python -m pytest` SHALL exit 0.

## FR-TEST-002
Each use case SHALL have a test using a mock or stub port implementation.

## FR-LINT-001
`ruff check .` SHALL exit 0 with no suppressed rules except documented exceptions.

## FR-LINT-002
`ruff format --check .` SHALL exit 0.

## FR-TYPE-001
`pyright` or `mypy` strict mode SHALL produce zero errors on the `domain/` and `application/` packages.
