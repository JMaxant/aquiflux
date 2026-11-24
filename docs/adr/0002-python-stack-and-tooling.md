# 0002. Use a modern Python backend stack, with uv, ruff, mypy and pytest

- **Status:** accepted
- **Date:** 2026-11-24

## Plain-language summary

The project is built in Python with widely used backend tools: FastAPI to serve data on the
web, SQLAlchemy to talk to the database, PostgreSQL to store data and, later, Elasticsearch for
search. Around the code, a small set of modern tools installs dependencies, checks the code's
style and correctness, and runs automated tests. These are mainstream, well-documented tools,
so what is learned here carries over to most Python backend projects.

## Context

The owner is an experienced PHP developer learning Python from scratch. The project must teach
idiomatic, modern Python backend development, not just "PHP written in Python", and cover the
usual concerns of a backend: HTTP APIs, a relational database, migrations, search, tests. The
front-end should stay light (decided separately, in phase 4).

## Options considered

### Option A: a modern Python backend stack

FastAPI, SQLAlchemy 2.0 + Alembic, PostgreSQL, Pydantic, httpx, Typer; tooling: uv, ruff, mypy,
pytest. **Pros:** mainstream and well documented; the tools share ideas (type hints drive Typer,
Pydantic and FastAPI alike), so learning compounds. **Cons:** many tools to discover at once.

### Option B: a "data science" stack

pandas, Jupyter notebooks, Streamlit. **Pros:** fast to get charts. **Cons:** teaches little
about backend engineering, testing or architecture, which is the learning goal.

### Option C: Django

**Pros:** batteries included, close to Symfony/Laravel habits. **Cons:** its all-in-one ORM and
conventions hide what SQLAlchemy and FastAPI make explicit, which matters when learning.

## Decision

Option A.

| Need | Tool | PHP equivalent |
|---|---|---|
| Python version, virtualenv, dependencies, lockfile | [uv](https://docs.astral.sh/uv/) | Composer (+ phpenv) |
| Formatting and linting | [ruff](https://docs.astral.sh/ruff/) | PHP-CS-Fixer + PHP_CodeSniffer |
| Static type checking | [mypy](https://mypy.readthedocs.io/) | PHPStan / Psalm |
| Tests | [pytest](https://docs.pytest.org/) (+ pytest-httpx) | PHPUnit / Pest |
| CLI | [Typer](https://typer.tiangolo.com/) | Symfony Console |
| HTTP client | [httpx](https://www.python-httpx.org/) | Guzzle / Symfony HttpClient |
| Validation, parsing | [Pydantic](https://docs.pydantic.dev/) | Symfony Serializer + Validator |
| ORM, migrations | [SQLAlchemy 2.0](https://docs.sqlalchemy.org/), [Alembic](https://alembic.sqlalchemy.org/) | Doctrine ORM + Migrations |
| Web API | [FastAPI](https://fastapi.tiangolo.com/) | Symfony / Slim |

Python 3.13. Type hints are mandatory everywhere and checked by mypy. pandas is deliberately
left out until phase 5 (data analysis); aggregations before that are done in SQL.

## Consequences

- Type hints are learned from day one, since FastAPI and Pydantic rely on them.
- ruff, mypy and pytest run in CI, so style and type errors block a merge.
- Each new library is introduced when a phase needs it, not upfront.
