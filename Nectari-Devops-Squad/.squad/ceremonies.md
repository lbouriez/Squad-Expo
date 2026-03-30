# Ceremonies — Raptor DevOps Team

> Structured team interactions that happen before or after work phases.

---

## Pre-Kickoff

| Field | Value |
|-------|-------|
| **Trigger** | manual + auto |
| **When** | before |
| **Condition** | any new feature, significant change, work touching 2+ agent domains, or any architecture decision |
| **Facilitator** | malcolm |
| **Participants** | malcolm, grant, + any-relevant |
| **Time budget** | focused |
| **Enabled** | ✅ yes |

**MANDATORY — nothing starts without this for feature work.**

**Agenda:**
1. Malcolm presents the feature/change request — what are we building and why?
2. Grant assesses technical impact — what systems are touched? what contracts need to be defined?
3. Identify which team members are affected (Arnold for pipelines? Wu for cloud? Muldoon for tooling?)
4. Define interfaces and contracts between components — written as decisions
5. Assign work to the right agents with clear boundaries
6. Document all contracts and decisions to `.squad/decisions/inbox/`

---

## Review Pipeline

| Field | Value |
|-------|-------|
| **Trigger** | auto |
| **When** | after |
| **Condition** | implementation complete — any code, script, pipeline, cloud resource, or tool change |
| **Facilitator** | grant |
| **Participants** | grant, harding, ellie |
| **Time budget** | thorough |
| **Enabled** | ✅ yes |

**Three sequential gates — each gates the next.**

**Stage 1 — Architect Review (Grant):**
- Reviews code quality, architecture alignment, contracts compliance, Azure/cloud best practices
- Validates that multi-component work uses the defined interfaces
- **APPROVES** → continue to Stage 2
- **REJECTS** → returns to original implementer with specific feedback → implementer fixes → retries
- **Second REJECTION** → ESCALATE TO LAURENT — do not attempt a third cycle

**Stage 2 — Documentation Gate (Harding):**
- Analyzes whether `.guidelines/` needs additions, updates, or removals
- Analyzes whether `../Documentation/Cloud` needs additions, updates, or removals
- Makes and implements documentation decisions independently
- Reports what was changed or why no changes were needed
- **Always runs** — even if nothing needs updating, Harding must confirm

**Stage 3 — QA Sign-Off (Ellie):**
- Manual testing, analysis, edge case validation
- Can run automated validation where available
- Can request fixes before approving — if fixes needed, they go back through Grant first
- **FINAL OK required** — nothing ships without Ellie's explicit sign-off
- This is the last gate — after Ellie approves, coordinator hands off to Laurent via `ask_user`

---

## Design Alignment

| Field | Value |
|-------|-------|
| **Trigger** | auto |
| **When** | before |
| **Condition** | multi-agent task involving 2+ agents modifying shared systems |
| **Facilitator** | grant |
| **Participants** | all-relevant |
| **Time budget** | focused |
| **Enabled** | ✅ yes |

**Agenda:**
1. Review the task and requirements
2. Agree on interfaces and contracts between components
3. Identify risks and edge cases
4. Assign action items

---

## Retrospective

| Field | Value |
|-------|-------|
| **Trigger** | auto |
| **When** | after |
| **Condition** | build failure, test failure, or reviewer rejection |
| **Facilitator** | grant |
| **Participants** | all-involved |
| **Time budget** | focused |
| **Enabled** | ✅ yes |

**Agenda:**
1. What happened? (facts only)
2. Root cause analysis
3. What should change?
4. Action items for next iteration
