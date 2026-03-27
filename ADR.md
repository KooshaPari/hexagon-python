# Architecture Decision Records — hexagon-python

## ADR-001: typing.Protocol for Port Interfaces

**Status:** Accepted

**Context:** Python supports multiple patterns for interface definition: `abc.ABC`, `typing.Protocol`, and informal duck typing.

**Decision:** Use `typing.Protocol` for port definitions. `abc.ABC` is used only when runtime `isinstance` checks on the port are required.

**Rationale:** `Protocol` enables structural subtyping — adapters do not need to explicitly inherit from the port class. This reduces coupling and makes test doubles trivial to write.

**Alternatives Considered:**
- `abc.ABC`: requires explicit inheritance; tighter coupling.
- Duck typing with no interface: no IDE support, no mypy checking.

**Consequences:** Static type checkers (mypy, pyright) enforce structural compatibility. Runtime `isinstance(adapter, SomePort)` requires `runtime_checkable` decorator.

---

## ADR-002: Pydantic for Domain Entities

**Status:** Accepted

**Context:** Python dataclasses lack validation. The template should demonstrate a pattern that is realistic for production use.

**Decision:** Use `pydantic.BaseModel` for domain entities where validation matters. Plain `@dataclass` is acceptable for simple value objects.

**Rationale:** Pydantic v2 is the standard for validated Python models in the Phenotype ecosystem. Its performance and ecosystem integration make it the default choice.

**Alternatives Considered:**
- `attrs`: similar functionality but less ecosystem adoption.
- Plain dataclasses: no validation, acceptable only for value objects.

**Consequences:** `pydantic` is a direct dependency of the domain package. This is the only external dependency permitted in `domain/`.

---

## ADR-003: uv as Package Manager

**Status:** Accepted

**Context:** Python has multiple package managers (pip, poetry, pdm, uv). The template must choose one.

**Decision:** Use `uv` (Astral) as the package manager. `pyproject.toml` is the single source of truth for dependencies and tool config.

**Rationale:** `uv` is the fastest Python package manager as of 2025, is pip-compatible, and is the Phenotype ecosystem standard per governance.

**Consequences:** Developers must install `uv`. CI uses `uv sync` instead of `pip install`.
