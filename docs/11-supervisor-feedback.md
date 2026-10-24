# 11. Supervisor Feedback

**Project:** Information system for optimizing collective food purchasing and food redistribution
**Supervisor:** Alibek Orynbek
**Review date:** 21 October 2026
**Reviewed:** `README.md`, `docs/01`–`docs/10`, `diagrams/`, repository history

---

## 1. Team and areas of responsibility

| Student | Role | Deliverables |
|---|---|---|
| Akbota Ospanali | Analyst — research and justification | 01 Proposal (jointly), 02 Evidence of relevance, 03 Literature review, 04 Existing systems |
| Zharkynay Mernibek | Architect / backend lead | 05 Technology comparison, 06 Requirements, 07 Architecture and diagrams, 09 Verification plan |
| Ibraim Karakat | UX and project management | 08 UX / prototype, 10 Project management and risks, 11 Supervisor feedback, README, presentation |

---

## 2. Assessment by criterion

All eleven criteria are met for the pre-defence. The comments in section 3 are development points for the next stage, not defects.

| # | Component | Verdict |
|---|---|---|
| 1 | Project proposal | Met. Problem, users, scope and four measurable objectives stated |
| 2 | Evidence of relevance | Met. 3 interviews (required 3–5), national statistics, findings separated from assumptions |
| 3 | Literature review | Met, above requirement. 16 sources, 12 scientific, structured analysis table, research gap |
| 4 | Existing systems | Met. 5 systems, 9 criteria, scored comparison |
| 5 | Technology comparison | Met, above requirement. 6 decisions, 2–3 alternatives each, weighted matrices |
| 6 | Requirements | Met. Functional and non-functional, MoSCoW priorities, acceptance criteria per requirement |
| 7 | Architecture and diagrams | Met. Context, use case, component and data model diagrams with sources and exports |
| 8 | UX / prototype | Met. Mockups of all key scenarios committed in `docs/prototype/` |
| 9 | Verification plan | Met. Tests T1–T7, metrics, usability test, baseline for comparison |
| 10 | Project management and risks | Met. Git repository, YouTrack project, responsibilities, milestones, risk register |
| 11 | Supervisor feedback | This document |

---

## 3. Development points for the next stage

| ID | Where | Point | Action | Owner | Task |
|---|---|---|---|---|---|
| SF-01 | `docs/02` | The sample meets the minimum of three interviews, but respondents are outside the primary target group, and Suppliers, Retailers and OSI/KSK representatives were not interviewed | Add five interviews: two low-income or large families, one supplier, one retailer, one OSI/KSK representative. Label the current round as exploratory | Akbota Ospanali | DIP-4 |
| SF-02 | `docs/02`, `docs/06` | Two findings run against the design: two of three respondents rejected near-expiry food, and two of three prefer home delivery while delivery is out of scope | Add a "Risks to adoption" subsection with a reasoned answer to each; both risks are recorded in the register | Akbota Ospanali | DIP-4 |
| SF-03 | `docs/09` | The 15 % savings objective has no measurement procedure: reference shops, basket composition, dates, averaging method | Define the protocol in section 9.4 and fix the three test baskets before the first measurement | Zharkynay Mernibek | DIP-15 |
| SF-04 | `docs/06`, `docs/08` | Actor naming differs: requirements use **Family**, prototype uses **Member** | Unify across documents, prototype and the diagram sources `01-system-context.dot`, `use-case.puml` | Zharkynay Mernibek | DIP-8, DIP-10 |
| SF-05 | `docs/08` | Image links point to `img/…`, the files are in `docs/prototype/`; the fifth screen is not referenced | Correct the paths and reference all five screens | Ibraim Karakat | DIP-14 |
| SF-06 | `src/` | Implementation has not started | Begin with the share allocation module, test-first. Tests T1–T7 already specify it; one subtask per test, Definition of Done: test passes and coverage ≥ 80 % | Zharkynay Mernibek, Ibraim Karakat | new task |
| SF-07 | `.gitignore`, `config/` | Stock Java template, while the stack is Java + Flutter + React; no configuration example | Extend `.gitignore`; add `config/.env.example` with placeholder values | Ibraim Karakat | DIP-1 |
| SF-08 | `docs/05`–`07` | Authors shown as "Student B (241755)", "by 241685" | Replace the numbers with names | Zharkynay Mernibek | DIP-13 |

---

## 4. Noted positively

- Traceability from objective to requirement to acceptance criterion to named test runs through the whole documentation set.
- `docs/03`: analysis table with a limitations column per source; the research gap is stated as three specific claims.
- `docs/05`: decision criteria linked to requirement IDs, trade-offs stated openly.
- Repository workflow: branch per task, pull requests, task IDs in commit messages, `.mailmap` unifying author identities.
- Documents 01, 02 and 06 were revised after the interviews, which shows the evidence fed back into the requirements.

---

## 5. Decision

Approved for the pre-defence. The points in section 3 are to be addressed in the next stage and presented with dates.

Follow-up review: 31 October 2026, covering the first implementation commits.

**How a point is closed:** branch `DIP-4-interviews` → commit `DIP-4: Add interviews with target group (SF-01)` → the row is marked Closed with the merge commit hash.

---

## 6. Change log

| Version | Date | Change |
|---|---|---|
| v0.1 | 24 October 2026 | Review of deliverables 1–11. All criteria met; eight development points raised for the next stage |