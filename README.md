# Information System for Optimizing Collective Food Purchasing and Redistribution

A web information system that helps groups of people organize joint food purchases and redistribute surplus food among members of a cooperative.

## Problem
Food cooperatives and neighbour groups usually coordinate purchases through messengers and spreadsheets. Orders get lost, quantities and costs are tracked manually, deadlines are missed, and leftover food is often thrown away because there is no simple way to offer it to others.

## Target users
- **Cooperative members** – join group purchases and claim surplus food.
- **Coordinators** – create purchases, collect orders and communicate with suppliers.
- **Administrators** – manage users and the cooperative.

## Expected outcomes
- One place to create, join and track group purchases.
- Automatic calculation of totals and each member's cost.
- A surplus board that lets members offer and claim food, reducing waste.

## Team and roles
| Member | GitHub | Role | Responsibility |
|---|---|---|---|
| Ospanali Akbota | [@akbota2007](https://github.com/akbota2007) | Analyst | Proposal, evidence of relevance, literature review, existing systems comparison |
| Mernibek Zharkynai | [@Zharrkynn](https://github.com/Zharrkynn) | Architect / backend lead | Technology comparison, requirements, architecture and diagrams, verification plan |
| Karakat Ibraim | [@Karakat177](https://github.com/Karakat177) | UX designer / project manager | Prototype, repository, project management and risks, supervisor feedback |

**Supervisor:** Orynbek Alibek

## Scope and status
**In scope:** user registration and roles; creating and joining group purchases; cost calculation; surplus board (offer and claim); notifications about purchase status.
**Out of scope:** online payments, delivery logistics, native mobile apps.

**Current status (pre-defense 1):** project proposal, evidence of relevance, literature review, system and technology comparisons, requirements, architecture diagrams, prototype, verification plan and project plan are prepared. Implementation starts next.

## Technologies
- Backend: Java, Spring Boot (REST API)
- Database: PostgreSQL
- Frontend: web application (responsive)
- Design and diagrams: clickable HTML prototype, UML/PlantUML
- Tools: Git and GitHub, YouTrack

## Links
- Repository: https://github.com/Karakat177/food-coop-diploma
- YouTrack: https://ibraimkarakat071.youtrack.cloud/projects/DIP
- Documentation: [docs/](docs/)
  - [Proposal](docs/01-proposal.md) · [Evidence of relevance](docs/02-evidence-of-relevance.md) · [Literature review](docs/03-literature-review.md)
  - [Existing systems](docs/04-existing-systems-comparison.md) · [Technology comparison](docs/05-technology-comparison.md)
  - [Requirements](docs/06-requirements.md) · [Architecture](docs/07-architecture.md) · [Prototype](docs/08-prototype.md)
  - [Verification plan](docs/09-verification-plan.md) · [Project management and risks](docs/10-project-management-risks.md) · [Supervisor feedback](docs/11-supervisor-feedback.md)
- Prototype: [prototype/index.html](prototype/index.html)

## Repository structure
`src/` source code · `docs/` documentation · `diagrams/` editable sources and exports · `config/` configuration examples

## Setup, run and test
Instructions will be added as soon as runnable code is available.