# Work Routing — Raptor DevOps Team

## Routing Table

| Work Type | Route To | Notes |
|-----------|----------|-------|
| New feature, tool evaluation, best practice question | Malcolm | Product Owner — understands what we need and what the DevOps world offers |
| Architecture decision, multi-component contract, pre-kickoff design | Grant | Mandatory for anything touching 2+ agent domains |
| Azure DevOps pipeline, GitHub Actions pipeline | Arnold | Sole pipeline owner — other agents propose, Arnold decides |
| Cloud scripts, ARM templates, Bicep, Azure Portal automation | Wu | Cloud automation owner |
| Testing, manual validation, QA sign-off | Ellie | Review gate — nothing ships without Ellie's OK |
| Terraform, auto code review tooling, cross-cutting DevOps tools | Muldoon | Expert DevOps — the catch-all for complex tooling |
| .guidelines/ documentation | Harding | Docs gate — analyzes additions/updates/removals |
| ../Documentation/Cloud documentation | Harding | Official cloud docs — same gate as .guidelines |
| Code review (architecture + standards) | Grant | Always first reviewer in review pipeline |
| Documentation review (guidelines + cloud docs) | Harding | Second reviewer in review pipeline |
| Final QA validation | Ellie | Third and final reviewer in review pipeline |
| Session logging, decisions merge | Scribe | Automatic — never needs routing |
| Escalation, final decision, ambiguous scope | Laurent | Human CTO — escalate after 2 failed attempts at any gate |
| Pre-kickoff ceremony | Malcolm + Grant + concerned members | Mandatory before any feature |

## Review Pipeline (Mandatory After Implementation)

```
[Implementation Complete]
        ↓
   Grant reviews
   (architecture, contracts, code standards)
        ↓ REJECT → return to implementer → retry
        ↓ REJECT again → ESCALATE TO LAURENT
        ↓ APPROVE
        ↓
  Harding reviews
  (docs impact: .guidelines + ../Documentation/Cloud)
        ↓ updates/flags as needed
        ↓ DONE
        ↓
   Ellie validates
   (testing, manual QA, edge case analysis)
        ↓ REJECT → return to implementer
        ↓ OK ← nothing ships without this
```

## Routing Rules

1. **ask_user MANDATORY** — coordinator must use `ask_user` at every handoff back to Laurent. Provide 2–4 concrete choices. No plain-text-only endings.
2. **Pre-Kickoff is MANDATORY** before any feature or significant cross-domain change. Malcolm + Grant must participate.
3. **Arnold owns all pipelines.** No other agent modifies pipeline files without Arnold's involvement.
4. **Harding owns all docs.** No other agent modifies .guidelines/ or ../Documentation/Cloud without Harding's review.
5. **Ellie's OK is non-negotiable.** Nothing ships without QA sign-off.
6. **Two consecutive rejections at any gate → escalate to Laurent**, not a third attempt.
7. **Scribe always runs** after any substantial work batch, always background, never blocks.
8. **When two agents could handle it**, pick the one whose domain is the primary concern.
9. **Eager by default** — spawn all agents who could usefully start work in parallel.
