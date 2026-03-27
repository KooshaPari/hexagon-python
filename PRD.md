# Product Requirements Document — hexagon-python

## Overview

`hexagon-python` is the canonical Python hexagonal architecture template for the Phenotype ecosystem. It provides a production-ready scaffold for Python services that enforces ports-and-adapters architecture, clean domain isolation, and idiomatic Python patterns using abstract base classes and dependency injection.

## Problem Statement

Python services in the Phenotype ecosystem lack a standardised hexagonal starting point. Without a template, each service mixes domain logic with infrastructure, making testing, refactoring, and governance enforcement difficult.

## Goals

- Provide a Python package scaffold with enforced hexagonal layer separation.
- Demonstrate Protocol / ABC-based port interfaces with dependency injection.
- Target Python 3.12+ with full type annotations.
- Include `pyproject.toml` with `ruff` linting and `pytest` testing configured.

## Non-Goals

- Does not implement production business logic.
- Does not ship an ASGI framework (FastAPI, Starlette) — adapters reference these as optional extras.
- Not a replacement for any Python framework.

## Epics & User Stories

### E1 — Scaffold Structure
- E1.1: `uv sync && python -m pytest` succeeds after cloning.
- E1.2: Package layout: `domain/`, `application/`, `ports/`, `adapters/` as Python sub-packages.
- E1.3: `pyproject.toml` defines build system, dependencies, and tool config.

### E2 — Domain Layer
- E2.1: Domain entities are Python dataclasses or Pydantic models with no infrastructure imports.
- E2.2: Domain errors are typed exception classes inheriting from a base `DomainError`.
- E2.3: Domain package has zero third-party imports beyond standard library and optionally Pydantic.

### E3 — Port Interfaces
- E3.1: Ports are defined as `typing.Protocol` or `abc.ABC` classes in `ports/inbound/` and `ports/outbound/`.
- E3.2: Async methods use `async def` in port definitions.

### E4 — Application Layer
- E4.1: Use case classes accept port instances via `__init__` parameters typed as port protocols.
- E4.2: Application package imports only `domain` and `ports`.

### E5 — Adapters
- E5.1: An in-memory outbound adapter implements the outbound port.
- E5.2: An inbound adapter stub (CLI or HTTP handler) exists.

### E6 — Testing
- E6.1: `pytest` passes with zero failures.
- E6.2: `ruff check .` and `ruff format --check .` pass with zero issues.

## Acceptance Criteria

- `uv sync && python -m pytest` succeeds.
- `ruff check .` exits 0.
- Import-linter config validates no cross-layer imports in domain or application.
