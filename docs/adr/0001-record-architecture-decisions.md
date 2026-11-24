# 0001. Record architecture decisions

- **Status:** accepted
- **Date:** 2026-11-24

## Plain-language summary

Every important technical choice in this project is written down in a short document called an
"architecture decision record" (ADR). Each one explains what was decided, which alternatives
were considered and why. Anyone joining the project, or reading it later, can understand the
reasoning without having to ask. Each record starts with a summary like this one, written for
non-technical readers.

## Context

This is a learning project that will grow over several phases, from a command-line tool to a
web dashboard. Many choices will be made along the way (tools, structure, data handling). Without
a record, the reasons behind them get lost, and decisions get reopened or contradicted. The
repository is public: showing *how* decisions were made is as valuable as the code.

## Options considered

### Option A: no formal record

Decisions live in commit messages, issues and memory. **Pros:** no overhead. **Cons:** reasoning
is scattered and quickly forgotten, and nothing shows it to a reader of the repository.

### Option B: a single design document

One long document updated over time. **Pros:** everything in one place. **Cons:** history is
overwritten, and it is hard to see when and why something changed.

### Option C: one short ADR per decision

Numbered Markdown files in `docs/adr/`, never rewritten; a new ADR supersedes an old one.
**Pros:** history is preserved, each decision is small and reviewable in a pull request.
**Cons:** a little writing discipline is needed.

## Decision

Option C, using a short variant of the [MADR](https://adr.github.io/madr/) format
(`0000-template.md`). Every ADR **must start with a plain-language summary** of 3 to 5 sentences
without jargon.

## Consequences

- A significant decision is not "done" until its ADR is merged (see the definition of done in
  `AGENTS.md`).
- Accepted ADRs are not edited, except for typos or to mark them as superseded.
- Writing ADRs is part of the learning: from ADR 0004 on, the project owner writes them.
