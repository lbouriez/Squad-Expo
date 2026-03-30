# Squad Templates

A collection of ready-to-use [Squad](https://github.com/bradygaster/squad) AI agent team templates.
Pick the squad that matches your project type, copy its folder, and start building.

**Last updated:** 2026-03-30

---

## What is this?

[Squad](https://github.com/bradygaster/squad) is an AI agent team framework for GitHub Copilot.
This repo is a **template library**: each subfolder is a self-contained squad ready to be copied
into a new project. Each project keeps its own memory and state — nothing is shared at runtime.

See the [team-state-storage pattern](https://bradygaster.github.io/squad/docs/scenarios/team-state-storage/)
for the recommended approach.

The `[CTO]` role is **Laurent** across all squads.

---

## Available Squads

### `Expo-Squad/` — React Native / Expo

Full-stack mobile development team for Expo projects.

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

---

### `Nectari-Devops-Squad/` — DevOps / Cloud Infrastructure (Jurassic Park universe)

DevOps and cloud automation team for Azure/GitHub Actions pipelines. No GitHub Issues integration.

| Name | Role |
|------|------|
| **Malcolm** | Product Owner |
| **Grant** | Architect & Code Reviewer |
| **Ellie** | QA Engineer |
| **Arnold** | Pipeline Engineer |
| **Wu** | Cloud Automation Engineer |
| **Muldoon** | Expert DevOps |
| **Harding** | Technical Writer |
| **Scribe** | Session Logger (silent) |

---

## Structure

Each squad folder follows this layout:

```
<Squad-Name>/
├── .copilot/
│   ├── mcp-config.json     # MCP tool configuration
│   └── skills/             # Copilot skills (29 shared skills)
├── .github/
│   ├── agents/             # squad.agent.md
│   └── workflows/          # Squad GitHub Actions workflows
└── .squad/
    ├── agents/             # Agent charters (and history.md)
    ├── casting/            # Casting policy (if applicable)
    ├── identity/           # wisdom.md, now.md
    ├── skills/             # Squad-specific skills
    ├── templates/          # Squad framework templates
    ├── ceremonies.md       # Team ceremonies
    ├── decisions.md        # Architectural decisions
    ├── routing.md          # Routing rules
    └── team.md             # Full team roster
```

---

## Using in a project

1. Clone or download this repo
2. Copy the squad subfolder that matches your project (e.g. `Expo-Squad/`)
3. Copy `.copilot/`, `.github/`, and `.squad/` from it into your new project root
4. Run `squad init` to register Squad with GitHub Copilot (if not already done)
5. Add project-specific skills to `.squad/skills/`
6. Remove agents you don't need from `team.md`

Each project keeps its own agent memory (`history.md`) and decisions — nothing is shared at runtime.

---

## Related

- [Squad documentation](https://bradygaster.github.io/squad/)
- [Squad GitHub](https://github.com/bradygaster/squad)
