# Information System for Optimizing Collective Food Purchasing and Redistribution

**FoodCoop KZ** — a platform where families in the same district pool their orders and buy staple food at wholesale prices directly from suppliers, and where local shops and bakeries sell food close to its expiry date at a discount instead of writing it off. Pilot: one district of Astana, Kazakhstan.

## Problem

In Kazakhstan food accounts for about 57 % of household consumer spending, against 10–15 % in developed countries, and prices of socially significant food products keep rising. Wholesalers and farmers sell cheaper, but their minimum order quantities — a 50 kg bag of flour, a case of oil — are too large for one low-income or large family to pay for and store.

At the same time the country generates about 1.7 million tonnes of food waste a year, and retailers find it cheaper to dispose of edible food than to donate it. Joint purchases are organised manually in messenger groups, with prepayment to one person and disputes over shares. No digital tool in Kazakhstan connects these two sides.

## Target users

| Actor | Who they are | What they need |
|---|---|---|
| **Family** | Large family, low-income household, targeted social assistance recipient or any resident | Buy staple food below retail price |
| **Pool organiser** | Building representative, head of a condominium association (OSI/KSK), active resident | Collect orders and payments without manual work, hand goods over |
| **Supplier** | Farmer, wholesaler, small distributor | Sell a large batch as one order |
| **Retailer / bakery** | Local shop or bakery | Sell near-expiry products instead of writing them off |
| **Administrator** | Platform team | Approve suppliers, verify social status, manage pick-up points |

## Objectives

1. Reduce the cost of a basket of socially significant food products for pool participants by **at least 15 %** against the average district retail price.
2. Let a new user create or join a pool in **no more than 3 minutes**.
3. Achieve **100 % correctness** of share and total calculations in all test scenarios.
4. Provide a fully bilingual interface in **Kazakh and Russian**.

## Expected outcomes

A working prototype — mobile application, supplier web portal and backend — tested on the purchase-pool and food-sharing scenarios, with savings and usability measured according to the verification plan.

## Scope

**In scope (MVP)**

- Family registration with district and building selection
- Supplier catalogue with wholesale prices, tiered prices and minimum order quantities
- Pool creation and joining, automatic calculation of each family's share, automatic closure when the target is reached
- Individual payment by Kaspi QR (sandbox) for every participant
- Combined order sent to the supplier once the pool is closed and paid
- Map of pick-up points
- Food-sharing module: retailers publish near-expiry products, families reserve them
- Supplier and retailer web portal
- "Social family" status with manual document verification by an administrator
- Baseline demand forecast for socially significant food products by district

**Out of scope**

- In-house delivery service and warehousing
- Live integration with government databases (eGov, targeted social assistance)
- Real payment processing — Kaspi QR runs in sandbox only
- Sale of alcohol, tobacco and medicines
- Multi-city launch

## Team and responsibilities

| Member | GitHub | Role | Responsibility |
|---|---|---|---|
| Akbota Ospanali | [@akbota2007](https://github.com/akbota2007) | Analyst — research and justification | Proposal, evidence of relevance, literature review, existing systems comparison, use case diagram, verification plan |
| Zharkynay Mernibek | [@Zharrrkynn](https://github.com/Zharrrkynn) | Architect / backend lead | Technology comparison, requirements specification, context and component diagrams, architecture description |
| Karakat Ibraim | [@Karakat177](https://github.com/Karakat177) | UX designer / project manager | Repository, README, UX prototype, project management and risks, supervisor feedback, release tags |

**Supervisor:** Alibek Orynbek

## Technologies

| Layer | Choice | Why |
|---|---|---|
| Backend | Java 21, Spring Boot 3 — modular monolith | Joining a pool, recalculating shares and creating payments must be one atomic transaction; `BigDecimal` gives exact money arithmetic |
| Database | PostgreSQL with PostGIS | Relational consistency for pools and payments; indexed distance queries for "pools within 2 km" |
| Mobile client | Flutter (Dart) | One codebase for Android and iOS, built-in localisation for Kazakh and Russian |
| Web portal | React (TypeScript) | Supplier, retailer and administrator interfaces; API client generated from the OpenAPI specification |
| Payments | Kaspi QR through an adapter (sandbox) | Dominant payment method in Kazakhstan; the adapter keeps the platform independent of one provider |
| Maps, notifications | 2GIS, Firebase Cloud Messaging | Pick-up points and pool map; push notifications and SMS codes |
| Demand forecast | Python (pandas, statsmodels) — offline job | Runs outside the backend, reads orders and writes forecasts |

Full comparison of alternatives: [docs/05-technology-comparison.md](docs/05-technology-comparison.md).

## Current status — probationary period 1

Documentation and design are complete: proposal, evidence of relevance, literature review, existing systems and technology comparisons, requirements, architecture and diagrams, UX prototype, verification plan, project management and risks, supervisor feedback.

Implementation has not started — `src/` contains the project structure only. The next stage begins with the share allocation module, written test-first against tests T1–T7 of the verification plan.

Submitted version: tag [`prob-period-1`](https://github.com/Karakat177/food-coop-diploma/tree/prob-period-1).

## Documentation

| # | Document |
|---|---|
| 1 | [Project proposal](docs/01-proposal.md) |
| 2 | [Evidence of relevance](docs/02-evidence-of-relevance.md) |
| 3 | [Literature review](docs/03-literature-review.md) |
| 4 | [Existing systems comparison](docs/04-existing-systems-comparison.md) |
| 5 | [Technology comparison](docs/05-technology-comparison.md) |
| 6 | [Requirements specification](docs/06-requirements.md) |
| 7 | [Architecture and diagrams](docs/07-architecture.md) |
| 8 | [UX / prototype](docs/08-prototype.md) |
| 9 | [Verification and evaluation plan](docs/09-verification-plan.md) |
| 10 | [Project management and risks](docs/10-project-management-risks.md) |
| 11 | [Supervisor feedback](docs/11-supervisor-feedback.md) |

## Links

- **Repository:** https://github.com/Karakat177/food-coop-diploma
- **YouTrack:** https://ibraimkarakat071.youtrack.cloud/issues/DIP — tasks DIP-1 … DIP-17
- **UX prototype mockups:** [docs/prototype/](docs/prototype/)
- **Diagram sources (editable):** [diagrams/source/](diagrams/source/) — Graphviz `.dot`, PlantUML `.puml`
- **Diagram exports:** [diagrams/export/](diagrams/export/) — PNG and SVG

## Repository structure

```
docs/          documentation, sections 01-11
docs/prototype/  UX mockups of the key user scenarios
diagrams/source/ editable diagram sources (.dot, .puml)
diagrams/export/ rendered diagrams (.png, .svg)
src/main/java/   backend source code
src/test/java/   tests
config/          configuration examples
```

## Way of working

Every work item is a YouTrack task `DIP-N` with an assignee, expected outcome, acceptance criteria and a deadline. Work is done in a branch `DIP-N-short-name`, commits start with `DIP-N:`, and changes reach `main` through a pull request reviewed by another team member. See [docs/10-project-management-risks.md](docs/10-project-management-risks.md).

## Setup, run and test

Instructions will be added as soon as runnable code is available.