# Squad-Expo

Shared [Squad](https://github.com/bradygaster/squad) configuration for Expo / React Native projects.
Provides a reusable AI agent team via upstream inheritance — no duplication across repos.

**Last updated:** 2026-03-27

---

## What is this?

[Squad](https://github.com/bradygaster/squad) is an AI agent team framework for GitHub Copilot.
This repo is a shared Squad upstream: add it to any Expo project and inherit the full team,
routing rules, decisions, and skills — without copying anything.

```bash
squad upstream add https://github.com/lbouriez/Squad-Expo.git --name platform --ref main
squad upstream sync platform
```

**What gets inherited by downstream projects:**

| Artifact | Location |
|----------|----------|
| Agent charters | `.squad/agents/*/charter.md` |
| Routing rules | `.squad/routing.md` |
| Ceremonies | `.squad/ceremonies.md` |
| Decisions (ADRs) | `.squad/decisions.md` |
| Team wisdom | `.squad/identity/wisdom.md` |
| Casting policy | `.squad/casting/policy.json` |
| Skills | `.squad/skills/*/SKILL.md` |

**What stays local in each project:**

- `team.md` — who the CTO is, which agents are active
- Agent memory (`history.md`, `history-archive.md`)
- Project-specific skills and decisions

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

The `[CTO]` role is filled per-project in each repo's local `team.md`.

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

1. Run `squad init` in your repo
2. Add this upstream:
   ```bash
   squad upstream add https://github.com/lbouriez/Squad-Expo.git --name platform --ref main
   squad upstream sync platform
   ```
3. Customize your local `team.md` (set CTO name, trim unused agents)
4. Add project-specific skills to `.squad/skills/`
5. Gitignore the runtime cache: add `.squad/_upstream_repos/` to `.gitignore`

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
