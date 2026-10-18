# Architecture and Diagrams

**Project:** Information system for optimizing collective food purchasing and food redistribution
**Owner:** Student B · **Status:** Draft v0.1
**Related:** Requirements (`06-requirements.md`, DIP-8), Technology comparison (`05-technology-comparison.md`, DIP-7)

| Section | Diagram | Task | Status |
|---|---|---|---|
| 1. System context | `diagrams/source/01-system-context.dot` | DIP-9 | Draft |
| 2. Use cases | `diagrams/source/02-use-case.*` | DIP-10 | Planned |
| 3. Components (draft) | `diagrams/source/03-component.*` | DIP-11 | Planned |
| 4. Architecture description | — | DIP-12 | Planned |

---

## 1. System context (DIP-9)

![System context diagram](../diagrams/export/01-system-context.png)

*Editable source:* [`diagrams/source/01-system-context.dot`](../diagrams/source/01-system-context.dot) (Graphviz).
*Exports:* [PNG](../diagrams/export/01-system-context.png), [SVG](../diagrams/export/01-system-context.svg).
*Regenerate:* `dot -Tpng -Gdpi=170 diagrams/source/01-system-context.dot -o diagrams/export/01-system-context.png`

The diagram treats the **Food Coop Platform** as a single black box and shows who uses it and which external systems it depends on. Its internal structure (mobile app, web portal, backend modules, database) is shown in the component diagram (section 3).

### 1.1 Actors

| Actor | Role in the system | Client used |
|---|---|---|
| Family | Joins purchase pools, pays its share, reserves food-sharing items | Mobile app |
| Pool Organizer | A family member or building representative who creates and manages a pool | Mobile app |
| Supplier | Publishes the wholesale catalog and fulfils consolidated orders | Web portal |
| Food-sharing Partner | Publishes surplus or near-expiry food | Web portal |
| Pickup Point Operator | Hands over orders and confirms pickup by scanning a QR code | Mobile app |
| Administrator / Moderator | Approves suppliers and partners, verifies social status documents | Web portal |

### 1.2 External systems

| System | Purpose | Integration in MVP |
|---|---|---|
| Kaspi QR | Generating payment QR codes and receiving payment confirmations | Mock adapter with the same interface. Real merchant access requires a registered legal entity |
| 2GIS | Map display and address geocoding for pools and pickup points | SDK / API (Google Maps as fallback) |
| Firebase | Push notifications (FCM) and SMS login codes (Phone Auth) | Real integration (free tier) |
| eGov / social assistance databases | Automatic verification of low-income status | **Not integrated** (Won't, FR-05). Replaced by document upload and manual moderation (FR-04) |

### 1.3 Interactions

| # | From → To | Data / action | Requirements |
|---|---|---|---|
| 1 | Family ↔ Platform | Browse catalog and nearby pools, join a pool, receive share amount and payment QR, reserve surplus food, receive notifications | FR-08, FR-10, FR-11, FR-17, FR-25 |
| 2 | Pool Organizer → Platform | Create a pool: supplier, products, target quantity, deadline, pickup point | FR-09 |
| 3 | Supplier ↔ Platform | Publish products, prices and minimum batches; receive consolidated orders; update order status | FR-06, FR-07, FR-19, FR-22, FR-28 |
| 4 | Food-sharing Partner → Platform | Publish surplus items with expiry date and pickup window | FR-24 |
| 5 | Pickup Point Operator → Platform | Confirm that a participant collected the order (QR scan) | FR-23 |
| 6 | Administrator → Platform | Approve supplier and partner accounts, verify status documents, block users, manage pickup points | FR-02, FR-04, FR-32, FR-33 |
| 7 | Platform ↔ Kaspi QR | Request a payment QR for each share; receive payment confirmation via webhook | FR-17, FR-18, NFR-06 |
| 8 | Platform → 2GIS | Load maps, convert addresses to coordinates | FR-03, FR-10 |
| 9 | Platform → Firebase | Send push notifications (pool filled, order ready); send SMS login codes | FR-01, FR-13, FR-22 |
| 10 | Platform ⇢ eGov | Not integrated in the MVP | FR-05 |

### 1.4 System boundary decisions

- **Payments are not processed by the platform itself.** The platform only creates payment requests and receives confirmations. Money moves inside Kaspi, which reduces security and legal requirements for the project.
- **Delivery is outside the system.** Suppliers deliver to pickup points by their own means. The platform only tracks the order status.
- **Status verification is manual.** Without access to state databases, a Moderator checks uploaded documents. Personal data is processed according to NFR-05.

---

## 2. Use cases (DIP-10)

*To be added.*

## 3. Components, draft (DIP-11)

*To be added.*

## 4. Architecture description (DIP-12)

*To be added.*
