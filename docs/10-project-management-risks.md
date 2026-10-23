# 10. Project Management and Risks

## Links
- Git repository: https://github.com/Karakat177/food-coop-diploma
- YouTrack project: https://ibraimkarakat071.youtrack.cloud/projects/DIP

## Way of working
Every work item is a YouTrack task (DIP-N) with an assignee, expected outcome and acceptance criteria. Work is done in a branch named `DIP-N-short-name`, commits start with `DIP-N:`, and changes reach `main` through a Pull Request reviewed by another team member. A task is closed only when its acceptance criteria are met.

## Responsibilities
| Member | Role | YouTrack tasks | Deliverables |
|---|---|---|---|
| Ospanali Akbota | Analyst | DIP-2, DIP-4, DIP-5, DIP-6 | Proposal, evidence of relevance, literature review, existing systems comparison |
| Mernibek Zharkynai | Architect / backend lead | DIP-7, DIP-8, DIP-9, DIP-10, DIP-11, DIP-12, DIP-15 | Technology comparison, requirements, diagrams, architecture description, verification plan |
| Karakat Ibraim | UX designer / project manager | DIP-1, DIP-3, DIP-13, DIP-14, DIP-16, DIP-17 | Repository setup, README, project management, prototype, supervisor feedback, pre-defense tag |

**Supervisor:** Orynbek Alibek. The supervisor reviews key deliverables and decisions (see `11-supervisor-feedback.md`).

## Milestones
| # | Milestone | Tasks | Date | Status |
|---|---|---|---|---|
| M1 | Project setup (repository, YouTrack, folder structure) | DIP-1 | 17 Oct 2026 | Done |
| M2 | Analysis: proposal, evidence, literature, system comparison | DIP-2, 4, 5, 6 | 20 Oct 2026 | Done |
| M3 | Requirements, technology choice, architecture, verification plan | DIP-7–12, 15 | 22 Oct 2026 | Done |
| M4 | Prototype, README, project management, supervisor review | DIP-3, 13, 14, 16 | 24 Oct 2026 | In progress |
| M5 | Final check and tag `pre-defense-1` | DIP-17 | 24 Oct 2026 | In progress |
| M6 | Core implementation | to be created | Nov 2026 | Planned |
| M7 | Remaining features, testing, evaluation | to be created | Dec 2026 | Planned |
| M8 | Final pre-defense and thesis text | to be created | Jan 2027 | Planned |

## Risks
| ID | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| R1 | Too little evidence from real users, so requirements rest on assumptions | Medium | High | Hold additional interviews; clearly separate verified findings from assumptions |
| R2 | Not enough time to implement all planned features | Medium | High | Prioritize requirements (must/should/could); build the core scenario first |
| R3 | Documents, diagrams and requirements become inconsistent | Medium | Medium | Cross-check at every pull request; review by another team member |
| R4 | Uneven contribution or commits not linked to the right account | Low | Medium | Task per person in YouTrack; each member commits from their own account; check contributors before each pre-defense |
| R5 | Chosen technologies prove too complex or unsuitable | Low | Medium | Build an early technical spike; keep alternatives from the technology comparison |

## Dependencies
- Architecture and diagrams (DIP-9, 10, 11, 12) depend on requirements (DIP-8).
- Requirements (DIP-8) depend on evidence of relevance (DIP-4) and the existing systems comparison (DIP-6).
- Technology comparison (DIP-7) depends on requirements, especially non-functional ones.
- Prototype (DIP-14) depends on the use case diagram (DIP-10).
- Verification plan (DIP-15) depends on requirements and acceptance criteria (DIP-8).
- Implementation depends on the technology choice (DIP-7) and the architecture (DIP-12).
- The final check (DIP-17) depends on all other tasks and merged pull requests.

## Next steps
1. Merge all open pull requests and tag `pre-defense-1`.
2. Create YouTrack tasks for implementation (M6) with assignees and deadlines.
3. Address supervisor comments and update the affected documents.
4. Hold additional interviews if the supervisor or committee asks for more evidence.