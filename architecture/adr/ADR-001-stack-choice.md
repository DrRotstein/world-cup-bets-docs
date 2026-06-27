---
id: ADR-001
title: Stack choice — NestJS + PostgreSQL + React on Railway
status: accepted
date: 2026-06-27
supersedes: null
superseded_by: null
---

## Context

The `world-cup-bets` project needs a full-stack web application for casual friend groups to bet on FIFA World Cup 2026 matches. Key constraints:

- **Deadline:** World Cup final is 2026-07-19; ship ASAP.
- **Team familiarity:** The user (Finn) is most experienced with NestJS (TS) + PostgreSQL + React deployed on Railway.
- **Scale:** Small friend groups (tens of users per group, not thousands). Low concurrency.
- **Non-goals:** No mobile native, no social network, no professional betting.

The user has expressed a **strong preference** for the above stack. There is no compelling technical reason to deviate — the stack is well-suited to the problem domain (server-rendered CRUD with real-time leaderboard, relational data with clear entities).

## Decision

We adopt the following stack:

| Layer | Technology | Version (stable at time of writing) |
|---|---|---|
| Backend runtime | Node.js 20 LTS | 20.x |
| Backend framework | NestJS | 10.x |
| Language | TypeScript | 5.x |
| ORM / DB access | Prisma | 5.x |
| Database | PostgreSQL | 16 |
| Frontend framework | React | 18.x |
| Frontend build | Vite | 5.x |
| Frontend routing | React Router | 6.x |
| HTTP client | TanStack Query + fetch | 5.x |
| Deploy target | Railway | — |
| External data | football-data.org API (v4) | free tier |

### Rationale for sub-choices

- **Prisma** over TypeORM: better type safety, auto-generated client, schema-as-code fits our ADR-driven workflow.
- **Vite** over CRA/Next.js: this is a SPA (no SEO needed for a private betting app); Vite is simpler and faster for pure client-side React.
- **TanStack Query** for server-state: caching, refetching, and optimistic updates out of the box.
- **Railway** for deploy: user familiarity + managed Postgres addon + simple PR previews.
- **football-data.org** as match data source: free tier covers FIFA World Cup; 10 req/min is adequate with server-side caching; the API has been stable since 2015.

## Consequences

### Positive

- Zero onboarding friction — user already knows the stack.
- NestJS provides structure (modules, DI, guards) that prevents the "Express spaghetti" anti-pattern.
- Prisma migrations + Railway's managed Postgres = simple schema evolution.
- Monorepo-friendly: both repos are TS, share tsconfig conventions.
- Railway deploy is push-to-deploy; no Docker required (though supported).

### Negative

- NestJS is opinionated — adds boilerplate for a small app. Acceptable trade-off for maintainability.
- Prisma cold-start on serverless can be slow. Railway uses containers (not serverless), so this is a non-issue.
- football-data.org free tier has a 10 req/min rate limit. Mitigated by caching match data server-side (matches update infrequently).

### Neutral

- PostgreSQL is arguably overkill for a small-scale app, but it's free on Railway's hobby tier and the user knows it.
- No SSR means the app won't be indexed by search engines. This is acceptable — the app is invite-only, not public-facing.

## Alternatives

### Alt A: Next.js full-stack (monolith)

- Pros: single deploy, SSR for free, API routes built in.
- Cons: user less familiar; mixing backend logic into Next.js API routes leads to entanglement; harder to separate concerns for a team.
- Rejected: user preference + separation of concerns.

### Alt B: Express.js + raw SQL

- Pros: minimal dependencies.
- Cons: no structure, no ORM type safety, no DI — leads to rot at scale.
- Rejected: NestJS provides the guardrails we want.

### Alt C: Supabase (BaaS)

- Pros: instant auth, real-time, managed Postgres.
- Cons: vendor lock-in, less control over business logic, user unfamiliar.
- Rejected: user wants full control + familiar stack.

## Related

- `docs/project/vision.md` — project constraints
- `docs/requirements/Q&A-onboarding.md` — user stack preference (Q9)
- `docs/tickets/EPIC-01.md` — this epic
