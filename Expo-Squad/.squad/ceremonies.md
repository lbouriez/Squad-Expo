# Ceremonies

> Structured checkpoints that happen before or after dev work. **Before ceremonies are BLOCKING** — dev work must not start until they complete and their output is injected into the dev agent's spawn prompt.

**Global handoff rule:** When a ceremony hands control back to the CTO or user, the coordinator uses `ask_user` with concrete next-step suggestions and a freeform option.

**Global logging rule:** After every ceremony that produces a brief, decision, or inbox file — if no immediate dev work starts — spawn Scribe in background immediately rather than waiting for a larger batch.

---

## 1. Pre-Dev Kickoff (BEFORE — BLOCKING)

| Field | Value |
|-------|-------|
| **Trigger** | auto |
| **When** | before any code changes |
| **Blocking** | ✅ YES — dev work cannot start until this ceremony completes |
| **Condition** | any task that will produce code changes |
| **Participants** | Morgan (always) · Howard (always) · Hollis (if UI changes) · Alex (if user-facing strings will change) · Manchas (if project has a Psychologue active) |
| **Time budget** | focused |
| **Enabled** | ✅ yes |

**Agenda:**

**Morgan (Product Owner):**
1. Read `.guidelines/` and any existing feature/spec docs for context
2. Validate the task aligns with product vision and existing features
3. Define scope: what's in, what's explicitly out, acceptance criteria
4. Produce a **Product Brief** (2–4 sentences: user goal, acceptance criteria, out-of-scope)

**Howard (Architect):**
1. Read `.guidelines/` relevant to the domain
2. Confirm the technical approach is sound
3. Identify risks, patterns to follow, interfaces to respect
4. Produce a **Technical Brief** (2–4 sentences: approach, constraints, patterns to follow)

**Hollis (UX — only if UI changes):**
1. Read task description and relevant existing screens/components
2. Produce a **UX Brief**: naming conventions, navigation flow, component reuse, accessibility notes

**Alex (i18n — only if user-facing strings will be added or modified):**
1. Identify all strings that will need i18n keys
2. Check existing locale files for keys to reuse or extend
3. Produce an **i18n Brief**: proposed key names, tone guidance, existing keys to reuse, namespace placement

**Manchas (Psychologue — only if active for the project):**
1. Review the task for any domain-sensitive implications (emotional impact, user safety, psychological appropriateness)
2. Produce a **Domain Brief**: any constraints, warnings, or guidance the dev agent must respect

**Output:** All briefs are combined and injected into every dev agent's spawn prompt. No dev work starts without this output.

**Escalation:** If Morgan cannot determine correct scope or behavior → escalate to the CTO before proceeding.

**Logging:** Scribe logs the combined brief to session artifacts immediately after kickoff, so it is recoverable if the session crashes mid-dev.

---

## 2. Interface Contract (BEFORE dev — BLOCKING for multi-agent tasks)

| Field | Value |
|-------|-------|
| **Trigger** | auto |
| **When** | after Pre-Dev Kickoff, before dev |
| **Blocking** | ✅ YES — dev work cannot start until contract is agreed |
| **Condition** | any task where 2+ dev agents will modify shared systems (e.g., backend API + frontend consumer, migration + seed data, shared data model from multiple layers) |
| **Facilitator** | Howard |
| **Participants** | Howard + all dev agents who will work on the task |
| **Time budget** | focused |
| **Enabled** | ✅ yes |

**Agenda:**
1. Review the task and identify all shared system boundaries (API shapes, DB keys, shared types, event contracts)
2. Produce an **Interface Contract**: exact TypeScript types for every API response and shared model that multiple agents will produce or consume
3. Identify risks and edge cases at the boundaries
4. Assign action items: each dev agent receives the contract + a clear list of what they own

**Output:** A short Interface Contract document injected into ALL dev agents' spawn prompts. No dev agent starts without it.

**Logging:** Scribe is spawned (background) immediately after this ceremony, logging the Interface Contract so it is recoverable if the session crashes.

---

## 3. Review Pipeline (AFTER dev — BLOCKING)

| Field | Value |
|-------|-------|
| **Trigger** | auto |
| **When** | after any dev agent completes code changes |
| **Blocking** | ✅ YES — QA cannot start until all applicable reviews pass |
| **Condition** | any agent produces code changes |
| **Participants** | see table below — run all applicable reviews in parallel |
| **Time budget** | focused |
| **Enabled** | ✅ yes |

**Review table (all applicable reviews run in parallel):**

| Review | Condition | Owner | Action on issue |
|--------|-----------|-------|-----------------|
| Architecture & code quality | Always | Howard | See issue handling below |
| i18n coverage | Project supports i18n AND user-facing strings changed | Alex | Alex applies minor fixes directly |
| UX review | Any UI element was added or changed | Hollis | See issue handling below |
| Android review | Native Android behavior may be affected | Keaton | See issue handling below |
| iOS review | Native iOS behavior may be affected | Vera | See issue handling below |
| Functional correctness | Always | Morgan | See issue handling below |
| Technical documentation | Always — check if `.guidelines/` is still accurate | Rob | Rob updates docs directly for minor gaps |
| End-user documentation | Project has user-facing docs AND user-facing behavior changed | Iris | Iris updates docs directly for minor gaps |
| Domain review | Project has a Psychologue (Manchas) active AND change touches domain-sensitive areas | Manchas | See issue handling below |

**Issue handling:**
- **Minor issue** (typo, small UX tweak, missing translation key, minor doc gap): the reviewing member fixes it directly without blocking or restarting the pipeline.
- **Major issue** (wrong architecture, broken behavior, missing i18n support, domain safety concern): route the specific issue back to the dev agent with exact instructions, then **repeat the full review pipeline from the top**.
- **Second major issue on the same change**: stop iterating — escalate to the CTO before continuing. Do not loop indefinitely.

**Logging:** Scribe is spawned (background) after every pipeline run — pass, fail, or fix cycle.

---

## 4. QA Sign-off (AFTER Review Pipeline passes — BLOCKING)

| Field | Value |
|-------|-------|
| **Trigger** | auto |
| **When** | after Review Pipeline passes |
| **Blocking** | ✅ YES — broken tests block ship; coverage gaps are advisory |
| **Condition** | any task that touched production code |
| **Participants** | Carrie (automated) · Quinn (manual/Playwright) — run in parallel |
| **Time budget** | focused |
| **Enabled** | ✅ yes |

**Carrie (Automation QA):**
0. **Clean install gate:** In each affected package root, run a clean dependency install without flags (`npm install` — no `--legacy-peer-deps`, no `--force`). If this fails with ERESOLVE or peer dep conflict, it is **BLOCKING** — stop and route back to the dev agent before running any tests.
1. **Build gate:** Run `tsc --noEmit` (or `npm run build`) on ALL packages that could be affected — not just the primary one. Must exit 0 before proceeding.
2. Review what changed and understand the new behavior
3. Run existing automated test suite — verify all tests pass
4. Assess whether new tests are needed based on the project's test policy
5. Write, update, or remove tests accordingly
6. Produce a **QA Report**: what was checked, what tests were added/updated, any gaps remaining

**Quinn (Manual QA):**
1. Open the running app using Playwright MCP
2. Navigate to and test every flow that was changed
3. Test for regressions in adjacent flows that could be affected
4. Produce screenshot evidence of each validated state
5. Produce a **Manual QA Report**: flows tested, screenshots attached, any issues found

**Blocking rule:** A broken existing test (Carrie) or a broken user flow (Quinn) is **BLOCKING** — treat as a major review issue and route back to the dev agent. The full Review Pipeline then restarts.

**Coverage gaps** (missing tests for new flows) are advisory — Carrie flags them but they do not block.

**Logging:** Scribe is spawned (background) after QA Sign-off — regardless of outcome.

---

## 5. Retrospective (AFTER failure)

| Field | Value |
|-------|-------|
| **Trigger** | auto |
| **When** | after |
| **Condition** | build failure, persistent test failure, or repeated reviewer rejection |
| **Facilitator** | coordinator |
| **Participants** | coordinator + all agents that worked on the failing task + CTO if architectural changes are needed |
| **Time budget** | focused |
| **Enabled** | ✅ yes |

**Agenda:**
1. What happened? (facts only)
2. Root cause analysis
3. What should change going forward?
4. Action items for next iteration

**Logging:** Scribe is spawned (background) after the Retrospective, capturing all action items and decisions.
