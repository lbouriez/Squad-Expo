# Squad Decisions

## Active Decisions

### ADR-001: Shared Squad for Expo projects
**Date:** 2026-03-27  
**Status:** Active  
**Decision:** Squad-Expo is a shared upstream Squad repository designed for Expo/React Native projects. It is not tied to any single project. Memory is always per-project (never shared via upstream). Agents, ceremonies, routing, and wisdom are shared.  
**Rationale:** ReKindle and Kidhoot share the same technology stack (Expo, React Native, EAS, Supabase/Firebase) and benefit from a consistent team structure. Maintaining two separate full squads would diverge rapidly.

---

### ADR-002: Howard owns architecture AND code review
**Date:** 2026-03-27  
**Status:** Active  
**Decision:** Howard (Architect) performs code review as part of the Review Pipeline. There is no separate Code Reviewer agent.  
**Rationale:** Separating architecture and code review created a gap where an agent could approve code that violated architectural decisions. Combining them in the Architect role ensures consistency.

---

### ADR-003: Review Pipeline is parallel, not sequential
**Date:** 2026-03-27  
**Status:** Active  
**Decision:** All applicable reviewers in the Review Pipeline (Howard, Alex, Hollis, Keaton, Vera, Morgan, Rob, Iris, Manchas) run in parallel after each dev cycle, not in a sequential chain.  
**Rationale:** Sequential reviews double or triple wall-clock time for multi-dimensional changes. Parallel review with a single restart (if major issues arise) is faster and equally thorough.

---

### ADR-004: QA is dual-track (automated + manual), both blocking
**Date:** 2026-03-27  
**Status:** Active  
**Decision:** QA Sign-off requires both Carrie (automation) and Quinn (manual Playwright) to pass. Both tracks are blocking. They run in parallel.  
**Rationale:** Automated tests miss visual regressions and interaction edge cases. Manual Playwright testing catches what unit/E2E tests miss. Both are required to ship with confidence.

---

### ADR-005: Manchas is a conditional agent
**Date:** 2026-03-27  
**Status:** Active  
**Decision:** Manchas (Psychologue) participates in every Pre-Dev Kickoff and every Review Pipeline run — but only when the project has explicitly activated a Psychologue role. Inactive by default.  
**Rationale:** Kidhoot requires child safety review for every screen. ReKindle requires couple dynamics review. Other future projects may not need domain psychology at all. Making Manchas conditional avoids ceremony bloat on projects that don't need it.

---

### ADR-006: No casting in the shared repo
**Date:** 2026-03-27  
**Status:** Active  
**Decision:** Casting (policy.json, registry.json) is project-specific and lives in each project's `.squad/casting/` directory. The shared Squad-Expo repo has no casting files.  
**Rationale:** Casting controls which model handles each agent, which may differ per project's API access, budget, and performance requirements. Sharing casting would impose one project's constraints on all others.

### ADR-007: ask_user is mandatory at every coordinator handoff
**Date:** 2026-03-27  
**Status:** Active  
**Decision:** The coordinator MUST use `ask_user` every time it hands control back to the CTO or user. This applies after every ceremony, after every work batch, after every review pipeline run, and after QA sign-off. Concrete next-step suggestions (2–4 choices) must be provided. Ending a turn with plain text output and no structured handoff is a violation of this rule.  
**Rationale:** Walls of text after agent work are disorienting. A structured `ask_user` prompt ensures the CTO stays in control of pace and direction, reduces cognitive load, and prevents the coordinator from silently continuing down a path that may not align with current priorities. This is the single most important UX rule for the squad.

---

## Governance

- All meaningful changes require team consensus
- Document architectural decisions here using the ADR format above
- Keep history focused on work, decisions focused on direction
