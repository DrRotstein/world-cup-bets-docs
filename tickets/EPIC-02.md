---
id: EPIC-02
type: epic
title: MVP Core — Groups, Betting, Leaderboard
parent: null
owner: project-lead
status: ready
priority: P0
estimate: L
created: 2026-06-27T12:21:00Z
acceptance:
  - "A user can sign up via Google OAuth in under 30 seconds"
  - "A user can create a group and invite friends via shareable link"
  - "World Cup match fixtures and results sync automatically from football-data.org"
  - "A user can place a score prediction on any upcoming match before kickoff"
  - "Bets lock at kickoff"
  - "A group leaderboard shows ranked members with correct point totals"
  - "Scoring: 4 pts exact score, 2 pts correct goal difference, 1 pt correct outcome, 0 wrong"
depends_on:
  - EPIC-01
blocks: []
---

## Context

This is the core product Epic. It delivers the complete MVP loop: sign up → join group → bet on matches → see leaderboard. Every story here is P0 — without any one of them, the product doesn't work.

Hard deadline: World Cup final 2026-07-19. No scope creep allowed.

## Scoring rules (user decision D-003)

- **4 points** — exact score predicted (e.g. predicted 2-1, result is 2-1)
- **2 points** — correct goal difference (e.g. predicted 3-1, result is 2-0 → difference of 2 matches)
- **1 point** — correct outcome only (predicted home win, got home win, but score/difference wrong)
- **0 points** — wrong outcome

## Stories

1. **S-01: Lightweight auth (Google OAuth)** — backend + frontend
2. **S-02: Groups & invite links** — backend + frontend
3. **S-03: Match data sync** — backend
4. **S-04: Place bets** — backend + frontend
5. **S-05: Leaderboard** — backend + frontend

## Non-goals (MVP)

- No chat or messaging between group members
- No push notifications
- No profile pages or avatars
- No multiple tournaments — World Cup 2026 only
- No admin panel

## Open questions

- (to be filled as team discovers them)
