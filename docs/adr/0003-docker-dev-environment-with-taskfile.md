# 0003. Run everything in Docker, driven by Task

- **Status:** accepted
- **Date:** 2026-11-24

## Plain-language summary

All the software the project needs (Python, the database, the tools) runs inside isolated
containers instead of being installed on the developer's computer. A single, simple command
tool ("Task") gives short, memorable commands such as `task test` to start, test or check the
project. Anyone, on any machine, gets the same environment in minutes, and the automated checks
on GitHub run exactly the same way.

## Context

The owner does not want to install and manage Python versions locally. The project needs a
PostgreSQL database from phase 2 and Elasticsearch in phase 6. Continuous integration (CI) must
behave like the local environment, otherwise "it works on my machine" problems appear. The owner
already uses and likes [Task](https://taskfile.dev).

## Options considered

### Option A: local install (pyenv/uv + local PostgreSQL)

**Pros:** fastest feedback, best IDE integration. **Cons:** pollutes the host, versions drift
between machines and CI.

### Option B: Docker Compose, commands typed by hand

**Pros:** isolated and reproducible. **Cons:** long `docker compose run --rm …` commands, easy
to get wrong.

### Option C: Docker Compose wrapped by Task

**Pros:** isolated and reproducible, with short commands; the same `task` commands run locally
and in CI. **Cons:** one more tool; the IDE needs extra setup to see the container's Python.

### Option D: Makefile instead of Task

**Pros:** available everywhere. **Cons:** awkward syntax, poor variable handling; the owner
prefers Task.

## Decision

Option C.

- **Official images only, as far as possible**: `postgres` for the database; the application
  image is a small Dockerfile based on an official image (the official `python` image with the
  official uv binary copied in, or Astral's official uv image that bundles Python). The owner
  writes this Dockerfile.
- Source code is mounted into the container as a volume, so edits are seen immediately.
- The container's virtual environment lives outside the mounted folder, so it never clashes with
  an optional host `.venv` used by the IDE.
- CI runs the same `task lint test` as a developer.

## Consequences

- Prerequisites on a machine: Docker and Task only.
- The IDE needs a Python interpreter to index code. If the JetBrains IDE in use cannot use a
  Docker interpreter, a uv-managed `.venv` on the host is used **for indexing only**; nothing is
  executed from it. Documented in `docs/dev-setup.md`.
- Commands are slightly slower than native ones (container start-up).
