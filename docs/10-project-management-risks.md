# 10. Project Management and Risks

**Project:** Information system for optimizing collective food purchasing and food redistribution
**Task:** DIP-13 · **Status:** v0.1 · 24 October 2026
**Supervisor:** Alibek Orynbek

## Links

- Git repository: https://github.com/Karakat177/food-coop-diploma
- YouTrack project: https://ibraimkarakat071.youtrack.cloud/projects/DIP
- Documentation index: [`README.md`](../README.md)

## Way of working

Every work item is a YouTrack task `DIP-N` with an assignee, expected outcome, acceptance criteria and a deadline. Work is done in a branch `DIP-N-short-name`, commits start with `DIP-N:`, and changes reach `main` through a pull request reviewed by another team member. A task is closed only when its acceptance criteria are met.

Supervisor comments are recorded in [`11-supervisor-feedback.md`](11-supervisor-feedback.md) as `SF-N` and are referenced from the commit that closes them.

## Responsibilities

| Member | Role | YouTrack tasks | Deliverables |
|---|---|---|---|
| Akbota Ospanali | Analyst — research and justification | DIP-2, DIP-4, DIP-5, DIP-6 | Proposal, evidence of relevance, literature review, existing systems comparison |
| Zharkynay Mernibek | Architect / backend lead | DIP-7, DIP-8, DIP-9, DIP-10, DIP-11, DIP-12, DIP-15 | Technology comparison, requirements, diagrams, architecture description, verification plan |
| Karakat Ibraim | UX designer / project manager | DIP-1, DIP-3, DIP-13, DIP-14, DIP-16, DIP-17 | Repository setup, README, project management, prototype, supervisor feedback, pre-defence tag |

Author identities in the git history are unified through `.mailmap` (DIP-1).

## Milestones

| # | Milestone | Tasks | Date | Status |
|---|---|---|---|---|
| M1 | Project setup: repository, YouTrack, folder structure | DIP-1 | 17 Oct 2026 | Done |
| M2 | Analysis: proposal, evidence, literature, system comparison | DIP-2, 4, 5, 6 | 20 Oct 2026 | Done |
| M3 | Requirements, technology choice, architecture, verification plan | DIP-7–12, 15 | 22 Oct 2026 | Done |
| M4 | Prototype, README, project management, supervisor review | DIP-3, 13, 14, 16 | 24 Oct 2026 | In progress |
| M5 | Final check and tag `pre-defense-1` | DIP-17 | 24 Oct 2026 | In progress |
| M6 | Core implementation: users, catalogue, purchase pools, share allocation | to be created | Nov 2026 | Planned |
| M7 | Surplus module, payments in sandbox, testing and evaluation | to be created | Dec 2026 | Planned |
| M8 | Final pre-defence and thesis text | to be created | Jan 2027 | Planned |

## Risks

| ID | Risk | Likelihood | Impact | Owner | Mitigation |
|---|---|---|---|---|---|
| R1 | Evidence comes from respondents outside the primary target group, so requirements rest partly on assumptions | Medium | High | Akbota Ospanali | Five additional interviews: two target families, one supplier, one retailer, one OSI/KSK representative (SF-01). Verified findings stay separated from assumptions |
| R2 | Users reject near-expiry food or expect home delivery, which the MVP does not provide | Medium | High | Akbota Ospanali | "Risks to adoption" subsection in `02-evidence-of-relevance.md` (SF-02); expiry window and storage conditions shown on every listing; delivery kept as an optional supplier service |
| R3 | The 15 % savings objective cannot be demonstrated because the measurement procedure is undefined | Medium | High | Zharkynay Mernibek | Protocol in `09-verification-plan.md` section 9.4: reference shops, fixed baskets, dates, averaging method; baskets fixed before the first measurement (SF-03) |
| R4 | Not enough time to implement all planned features | Medium | High | all | MoSCoW priorities; the core purchase scenario first; Could-items dropped before Must-items |
| R5 | Documents, diagrams and requirements drift apart | Medium | Medium | Zharkynay Mernibek | Cross-check at every pull request; actor names verified against `06-requirements.md` (SF-04) |
| R6 | Uneven contribution, or commits not attributed to the right account | Low | Medium | Karakat Ibraim | One task per person in YouTrack; `.mailmap` in place; contributors checked before each pre-defence |
| R7 | Chosen technologies prove too complex for the team | Low | Medium | Zharkynay Mernibek | Early technical spike on the share allocation module; alternatives from `05-technology-comparison.md` kept open |
| R8 | Kaspi QR sandbox is unavailable or its terms change | Low | Medium | Zharkynay Mernibek | Payment provider hidden behind an adapter (Decision 6); a stub payment provider is used if the sandbox is unavailable |

## Dependencies

- Requirements (DIP-8) depend on evidence of relevance (DIP-4) and the existing systems comparison (DIP-6).
- Technology comparison (DIP-7) depends on requirements, especially non-functional ones.
- Architecture and diagrams (DIP-9, 10, 11, 12) depend on requirements (DIP-8).
- Prototype (DIP-14) depends on the use case diagram (DIP-10).
- Verification plan (DIP-15) depends on requirements and their acceptance criteria (DIP-8).
- Implementation (M6) depends on the technology choice (DIP-7) and the architecture (DIP-12).
- Final check (DIP-17) depends on all other tasks and merged pull requests.

## Next steps

1. Merge the open pull requests and tag `pre-defense-1` (DIP-17).
2. Create YouTrack tasks for M6 with assignees, acceptance criteria and deadlines; one subtask per test T1–T7.
3. Close the supervisor's points SF-01 … SF-08 and update the affected documents.
4. Hold the five additional interviews (R1) and extend `02-evidence-of-relevance.md`.