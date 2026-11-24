# aquiflux

**From rainfall to groundwater: French open data explorer.**

`aquiflux` collects groundwater levels from the [Hub'Eau](https://hubeau.eaufrance.fr) API
(and, later, Météo-France weather data) for a French *département*, stores them, and shows how
aquifers respond to rain.

It is also a learning project: built step by step to learn Python, FastAPI, SQLAlchemy,
PostgreSQL and Elasticsearch. See [`docs/learning/`](docs/learning/) for the journey.

## Status

| Phase | Scope | Status |
|---|---|---|
| 0 | Foundations: Docker, Taskfile, tooling, CI, first TDD exercise | 🚧 in progress |
| 1 | CLI: fetch stations and measurements from Hub'Eau | ⏳ |
| 2 | Storage: PostgreSQL, SQLAlchemy, Alembic, incremental ingestion | ⏳ |
| 3 | Read-only API with FastAPI | ⏳ |
| 4 | Dashboard: server-rendered pages, HTMX, ECharts | ⏳ |
| 5 | Météo-France data and rainfall/groundwater analysis | ⏳ |
| 6 | Elasticsearch: station search and geographic queries | ⏳ |

## Quick start

Requirements: [Docker](https://docs.docker.com/get-docker/) and [Task](https://taskfile.dev).
Nothing else is installed on your machine.

Commands will be documented here once the dev environment exists (phase 0).

## Documentation

- [`CONTEXT.md`](CONTEXT.md): the domain and its vocabulary
- [`docs/architecture.md`](docs/architecture.md): how the code is organised
- [`docs/dev-setup.md`](docs/dev-setup.md): setting up a development environment
- [`docs/adr/`](docs/adr/): architecture decision records
- [`docs/learning/`](docs/learning/): learning journal, one page per phase

## License

[MIT](LICENSE)
