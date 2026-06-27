---
id: EPIC-01
type: epic
title: Onboarding & stack selection
parent: null
owner: architect
status: ready
priority: P0
estimate: S
created: 2026-06-27T10:50:00Z
acceptance:
  - "ADR-001 exists and is approved, selecting the stack per vision.md constraints"
  - "docs/architecture/overview.md exists with a one-page system sketch"
  - "Backend repo contains an empty README and .gitignore"
  - "Frontend repo contains an empty README and .gitignore"
depends_on: []
blocks: []
---

## Context

This is the bootstrap Epic. The team cannot proceed until the architect has selected a stack (ADR-001) and produced an overview. Vision, Q&A, and non-goals are attached.

User has a strong preference for NestJS (TS) + PostgreSQL + React on Railway. Architect should respect this unless there's a compelling reason to deviate (document in ADR-001).

## Scope

- Choose stack consistent with user preference (NestJS/TS + PostgreSQL + React + Railway).
- Sketch a one-page system overview (frontend, backend, DB, external match data source).
- Initialize both code repo skeletons (README, license placeholder, .gitignore).
- Identify a reliable match data source for the 2026 World Cup (addresses risk R-2).

## Non-goals

- No feature work this Epic.
- No DB schema yet — that belongs to the first feature Epic.

## Open questions

- (filled as architect discovers them via `question` messages)
