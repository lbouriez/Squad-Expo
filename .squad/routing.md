# Work Routing

How to decide who handles what.

## Routing Table

| Work Type                                                                 | Route To   | Examples                                                                                 |
| ------------------------------------------------------------------------- | ---------- | ---------------------------------------------------------------------------------------- |
| Product vision, feature specs, functional validation, roadmap             | Morgan     | Feature spec writing, acceptance criteria, "does this match what we asked for?"          |
| Architecture decisions, interface contracts, code review, tech debt       | Howard     | API contracts, parallel-dev interface definitions, code quality, architecture direction  |
| Backend API, services, repositories, DI, Zod schemas, Prisma, migrations  | Stan       | New endpoints, DI registration, migrations, integration tests                            |
| Chatbot system, conversation logic, tool definitions, streaming, memory   | Joel       | New tools, ChatService, tool architecture, message history                               |
| AI providers, model selection, prompt engineering, cost tracking          | Mary       | AI router, provider abstraction, model evaluation, cost optimization                     |
| Expo / React Native screens, components, hooks, offline patterns          | Clementine | New screens, UI components, React Query hooks, error handling, performance               |
| CI/CD, GitHub Actions, Docker, deployment, secrets, monitoring            | Patrick    | Pipeline fixes, deploy config, environment variables, health checks, Sentry              |
| Sentry triage: scan production errors, categorize, recommend fixes        | Patrick    | "run a Sentry triage", "check production errors", "what's broken in prod?"               |
| Android native config, Gradle, EAS Android, Play Store, APK signing       | Keaton     | Gradle failures, manifest issues, FCM setup, EAS Android profiles, Play Store submission |
| iOS native config, Xcode, EAS iOS, APNs, App Store, provisioning          | Vera       | Xcode build failures, APNs setup, code signing, EAS iOS profiles, App Store submission   |
| UX quality, design system, accessibility, color tokens, interaction flows | Hollis     | Hardcoded color audits, tap targets, a11y, UX flow review, brand consistency             |
| i18n quality, locale coverage, copy accuracy, RTL, pluralization          | Alex       | Locale coverage (all configured languages), translation accuracy, App Store metadata     |
| Automated tests: E2E, unit, integration — writing, maintaining, gating    | Carrie     | Playwright E2E, RNTL unit tests, coverage enforcement, offline scenario testing          |
| Live manual testing via Playwright MCP, navigation flows, screenshots     | Quinn      | Browser-based UI validation, regression walkthroughs, screenshot evidence                |
| Technical documentation: .guidelines/, architecture docs, index upkeep    | Rob        | .guidelines/ audits, doc creation, index.md maintenance, removing stale docs             |
| End-user documentation: website, user guides, App Store copy, FAQs        | Iris       | User-facing docs, onboarding content, release notes, App Store descriptions              |
| Domain psychology review: safety, appropriateness, user wellbeing         | Manchas    | Safety gates, content review, age-appropriateness, psychological risk assessment         |
| Session logging                                                           | Scribe     | Automatic — never needs routing                                                          |
| Work queue monitoring                                                     | Ralph      | Triggered by coordinator or auto-loop                                                    |

## Issue Routing

| Label              | Action                                               | Who        |
| ------------------ | ---------------------------------------------------- | ---------- |
| `squad`            | Triage: analyze issue, assign `squad:{member}` label | Howard     |
| `squad:morgan`     | Product vision, feature specs, functional validation | Morgan     |
| `squad:howard`     | Architecture, interface contracts, code review       | Howard     |
| `squad:stan`       | Backend API, services, DB, DI, tests                 | Stan       |
| `squad:joel`       | Chatbot tools, conversation logic, streaming         | Joel       |
| `squad:mary`       | AI providers, model selection, prompts, cost         | Mary       |
| `squad:clementine` | Frontend screens, components, hooks                  | Clementine |
| `squad:patrick`    | CI/CD, deployment, infra, monitoring, Sentry         | Patrick    |
| `squad:keaton`     | Android platform, Gradle, EAS Android, Play Store    | Keaton     |
| `squad:vera`       | iOS platform, Xcode, EAS iOS, App Store              | Vera       |
| `squad:hollis`     | UX, design system, a11y, color tokens                | Hollis     |
| `squad:alex`       | i18n, locale coverage, translation accuracy          | Alex       |
| `squad:carrie`     | Automated tests, E2E, unit, coverage                 | Carrie     |
| `squad:quinn`      | Manual browser testing, Playwright MCP               | Quinn      |
| `squad:rob`        | Technical documentation, .guidelines/                | Rob        |
| `squad:iris`       | End-user docs, website, App Store copy               | Iris       |
| `squad:manchas`    | Domain safety review, content appropriateness        | Manchas    |

### How Issue Assignment Works

1. When a GitHub issue gets the `squad` label, **Howard** triages it — analyzing content, evaluating complexity, assigning the right `squad:{member}` label, and commenting with triage notes.
2. When a `squad:{member}` label is applied, that member picks up the issue in their next session.
3. Members can reassign by removing their label and adding another member's label.
4. The `squad` label is the "inbox" — untriaged issues waiting for Howard's review.
5. **@copilot evaluation:** Howard checks if the issue matches @copilot's capability profile (🟢 good fit / 🟡 needs review / 🔴 not suitable). If it's a good fit, Howard may route to `squad:copilot` instead.

## Review Gates (Required Before Ship)

All review requirements are defined in **Rule 5** of the Rules section below. The review pipeline runs after every code change and includes architecture, i18n, UX, platform (Android/iOS), functional, tech doc, end-user doc, and psychologue reviews — in parallel where conditions apply. QA (automated + manual) runs after all reviews pass (Rule 6).

## Rules

1. **Pre-dev ceremonies are BLOCKING.** A Pre-Dev Kickoff must complete before any dev agent starts work. For tasks where multiple dev agents touch shared systems, an Interface Contract must be produced and injected into every dev agent's spawn prompt before dev starts. Ceremony details and participants are defined in `ceremonies.md`. If scope cannot be determined from existing documentation → escalate to the CTO before proceeding.

2. **Scribe is MANDATORY** after every agent work batch and every coordinator-only turn that writes to `.squad/decisions/inbox/`. Spawn Scribe as `mode: "background"` immediately after collecting results. The only exception: zero agents ran and zero inbox files exist.

3. **Quick facts → coordinator answers directly.** Don't spawn an agent for trivial lookups.

4. **"Team, ..." → fan-out.** When the CTO or coordinator addresses the full team, spawn all relevant agents simultaneously as `mode: "background"`.

5. **Review pipeline (mandatory after any code change):**

   The following reviews are required after any agent produces code changes. All reviews that apply must run in parallel:

   | Review                      | Condition                                                                           | Owner   |
   | --------------------------- | ----------------------------------------------------------------------------------- | ------- |
   | Architecture & code quality | Always                                                                              | Howard  |
   | i18n coverage               | If project supports i18n AND user-facing strings changed                            | Alex    |
   | UX review                   | If any UI element was added or changed                                              | Hollis  |
   | Android review              | If native Android behavior may be affected                                          | Keaton  |
   | iOS review                  | If native iOS behavior may be affected                                              | Vera    |
   | Functional correctness      | Always                                                                              | Morgan  |
   | Technical documentation     | Always — check if `.guidelines/` is still accurate; add/update/remove as needed     | Rob     |
   | End-user documentation      | If project has user-facing docs AND user-facing behavior changed                    | Iris    |
   | Domain safety review        | If Manchas is active for this project AND the change touches domain-sensitive areas | Manchas |

   **Issue handling during review:**
   - **Minor issue** (typo, missing translation, small UX tweak): the reviewing member fixes it directly without restarting the pipeline.
   - **Major issue** (wrong architecture, broken behavior, missing i18n support): route back to the dev agent with exact instructions, then repeat the full review pipeline from the top.
   - **Second major issue on the same change**: stop iterating — escalate to the CTO before continuing.

6. **QA phase (after all reviews pass):**

   Run both QA tracks in parallel:
   - **Automation QA**: verify that existing automated tests still pass; assess whether new tests are needed based on the project's test policy; write, update, or remove tests accordingly.
   - **Manual QA**: use Playwright MCP to open the running app in a browser and validate everything that changed — new features, modified flows, regression of existing behavior. Produce screenshot evidence.

   If Automation QA finds a broken test → BLOCKING (treat as a major review issue, re-route to dev).
   If Manual QA finds a broken flow → BLOCKING (treat as a major review issue, re-route to dev).

7. **Psychologue gate:** If the project has a Psychologue (Manchas) configured, Manchas participates in every Pre-Dev Kickoff AND every review pipeline, not just safety-critical changes.

8. **Every coordinator handoff uses `ask_user`.** Present 2–4 concrete next-step suggestions when returning control to the CTO. Always include a freeform option.
