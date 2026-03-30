# Squad Decisions — Raptor DevOps Team

## Active Decisions

### 2026-03-30: ask_user Mandatory at Every Coordinator Handoff
**By:** Laurent (CTO)
**What:** The coordinator MUST use `ask_user` every time it hands control back to Laurent or the user. This applies after every ceremony, after every work batch, after every review pipeline run, and after QA sign-off. Concrete next-step suggestions (2–4 choices) must be provided. Ending a turn with plain text output and no structured handoff is a violation of this rule.
**Why:** Walls of text after agent work are disorienting. A structured `ask_user` prompt ensures Laurent stays in control of pace and direction, reduces cognitive load, and prevents the coordinator from silently continuing down a path that may not align with current priorities. This is the single most important UX rule for the squad.

### 2026-03-30: Pre-Kickoff Ceremony is Mandatory
**By:** Laurent (CTO)
**What:** Pre-Kickoff ceremony is MANDATORY before any feature or significant cross-domain work. Malcolm (PO) and Grant (Architect) must always participate. Other members are added based on scope.
**Why:** Ensures contracts are defined before work begins, preventing rework and misalignment.

### 2026-03-30: Review Pipeline Gate Order — Grant → Harding → Ellie
**By:** Laurent (CTO)
**What:** All implementation work must pass through: (1) Grant for architecture/code review, (2) Harding for documentation impact assessment, (3) Ellie for QA sign-off. Two consecutive rejections at any single gate trigger escalation to Laurent — no third attempt.
**Why:** Ensures quality, documentation, and functional validation are all independently checked. Two failures means the issue needs human judgment.

### 2026-03-30: Arnold Owns All Pipelines
**By:** Laurent (CTO)
**What:** Arnold is the sole owner of all Azure DevOps and GitHub Actions pipeline definitions. No other agent modifies pipeline files without Arnold's involvement.
**Why:** Pipelines are critical infrastructure — single ownership prevents conflicting changes.

### 2026-03-30: Harding Owns All Documentation
**By:** Laurent (CTO)
**What:** Harding is the sole decision-maker for `.guidelines/` and `../Documentation/Cloud`. No other agent modifies these without Harding's review and approval.
**Why:** Documentation consistency requires a single voice.

### 2026-03-30: No GitHub Issues Integration
**By:** Laurent (CTO)
**What:** This squad does not use GitHub Issues mode or Ralph (Work Monitor). The team works from direct user requests and internal task management.
**Why:** The DevOps team's work intake is managed directly, not through GitHub issues.

## Governance
- All meaningful changes require team consensus
- Document architectural decisions here
- Keep history focused on work, decisions focused on direction
- Laurent has final say on all escalations
