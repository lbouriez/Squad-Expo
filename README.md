# Squad-Expo

Shared [Squad](https://github.com/bradygaster/squad) configuration for Expo / React Native projects.
A ready-to-use AI agent team — copy it into any new Expo project to hit the ground running.

**Last updated:** 2026-03-27

---

## What is this?

[Squad](https://github.com/bradygaster/squad) is an AI agent team framework for GitHub Copilot.
This repo is a **shared team baseline**: copy the `.squad/` folder into a new project and customize
from there. Each project keeps its own memory and state — nothing is shared at runtime.

See the [team-state-storage pattern](https://bradygaster.github.io/squad/docs/scenarios/team-state-storage/)
for the recommended approach.

---

## The Team

| Name | Role |
|------|------|
| **Morgan** | Product Owner |
| **Howard** | Architect + Code Reviewer |
| **Clementine** | Frontend Developer |
| **Stan** | Backend Developer |
| **Hollis** | UX Designer |
| **Alex** | i18n Specialist |
| **Keaton** | Android Platform Expert |
| **Vera** | iOS Platform Expert |
| **Carrie** | Automation QA Engineer |
| **Quinn** | Manual QA (Playwright MCP) |
| **Patrick** | DevOps / Infrastructure |
| **Joel** | AI Chatbot Expert |
| **Mary** | AI / ML Expert |
| **Rob** | Technical Documentation Writer |
| **Iris** | End User Documentation Writer |
| **Manchas** | Domain Safety (Psychologue) |
| **Scribe** | Session Logger (silent) |
| **Ralph** | Work Monitor |

The `[CTO]` role is **Laurent** across all projects.

---

## Structure

```
.squad/
├── agents/          # 18 agent charters (generic, no project-specific paths)
├── casting/         # Casting policy
├── identity/        # wisdom.md (shared patterns)
├── skills/          # Shared skills (guidelines-reference)
├── ceremonies.md    # 5 ceremonies: kickoff, contract, review pipeline, QA, retro
├── decisions.md     # ADR-001 through ADR-007
├── routing.md       # 8 routing rules incl. parallel review pipeline + mandatory ask_user
└── team.md          # Full team roster with [CTO] placeholder
```

---

## Using in a project

1. Clone or download this repo
2. Copy the `.squad/` folder into your new project
3. Run `squad init` to register Squad with GitHub Copilot (if not already done)
4. Add project-specific skills to `.squad/skills/`
5. Remove agents you don't need from `team.md`

Each project keeps its own agent memory (`history.md`) and decisions — nothing is shared at runtime.

---

## ADRs

| # | Decision |
|---|----------|
| ADR-001 | Shared Squad for Expo projects — single upstream, memory stays local |
| ADR-002 | Howard owns architecture + code review gate |
| ADR-003 | Parallel review pipeline (up to 9 reviewers run simultaneously) |
| ADR-004 | Dual-track QA — Carrie (automation) + Quinn (manual Playwright) both blocking |
| ADR-005 | Manchas is conditional — only triggered for emotionally sensitive content |
| ADR-006 | No casting files in shared repo — casting is always project-specific |
| ADR-007 | `ask_user` is mandatory at every coordinator handoff — never assume |

---

## Related

- [Squad documentation](https://bradygaster.github.io/squad/)
- [Squad GitHub](https://github.com/bradygaster/squad)
