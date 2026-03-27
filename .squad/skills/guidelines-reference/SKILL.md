---
name: "guidelines-reference"
description: "Navigate and use the project's .guidelines/ directory — find the right guideline for any task"
domain: "project-conventions"
confidence: "high"
---

## Context

Every project using this squad has a `.guidelines/` directory at the repo root. This is the single source of truth for all coding conventions, patterns, and rules. Before starting any work, agents must read the relevant guideline file for their domain.

For workflow guidance, prefer domain-specific skills if available (e.g., `api`, `backend-workflow`, `frontend-workflow`).

## How to Navigate Guidelines

### 1. Start with the index
```
.guidelines/index.md    ← always start here; full map of available guidelines
```

### 2. Common subdirectory conventions
Most projects organize `.guidelines/` like this — but always verify with `index.md`:

```
.guidelines/
├── index.md            # Master navigation — read first
├── backend/            # Backend patterns (services, repos, DI, schemas, routes, testing)
├── frontend/           # Frontend patterns (theming, i18n, components, screens, routing)
├── shared/             # Cross-project rules (logging, versioning, file organization)
├── features/           # Feature documentation (project-specific)
└── deployment/         # EAS Build, App Store, CI/CD
```

### 3. Quick search strategy
1. **By domain** → open the relevant index file (e.g., `backend/backend-index.md`, `frontend/frontend-index.md`)
2. **By keyword** → search `.guidelines/` for terms like `theme`, `i18n`, `prisma`, `DI`
3. **By task** → find the `{domain}-checklist.md` file for a full task checklist

## Critical Rules (Expo/React Native projects)

These rules apply to all projects using this squad. Specific implementations vary by project — check the project's `.guidelines/` for the exact API.

**Backend:**
- ❌ Never `console.log` → ✅ use the project's structured logger
- ❌ Never skip DI registration → ✅ always register in identifiers + module
- ✅ Always `@injectable()` on services and repositories
- ✅ Always Zod schemas with `.openapi()` metadata

**Frontend:**
- ❌ Never hardcode colors → ✅ use the project's theme system
- ❌ Never hardcode text → ✅ use the project's i18n hook
- ❌ Never relative imports → ✅ use `@/` path aliases
- ✅ Always React Query for server state
- ✅ Always Zustand for client state
- ✅ Always add `testID` to interactive elements

## When a Guideline is Missing

If no guideline file exists for a topic:
1. Check `.guidelines/shared/` for cross-domain rules
2. Ask the coordinator — the CTO may need to create the guideline before work starts
3. Never invent conventions without checking `.guidelines/index.md` first
