# Requirements Specification

**Project:** Information system for optimizing collective food purchasing and food redistribution
**Task:** DIP-8 · **Owner:** Student B · **Status:** Draft v0.2 (aligned with DIP-2, DIP-4, DIP-6, DIP-10, DIP-15; to be refined after interview results)
**Based on:** Project proposal (`01-proposal.md`, DIP-2), Evidence of relevance (`02-evidence-of-relevance.md`, DIP-4), Existing systems comparison (`04-existing-systems-comparison.md`, DIP-6)
**Used by:** Technology comparison (DIP-7), diagrams (DIP-9, DIP-10, DIP-11), UX prototype (DIP-14), Verification plan (`09-verification-plan.md`, DIP-15)

---

## 1. Purpose and scope

The system lets families living in the same district or building join **purchase pools** and buy socially significant food products (SSFP) directly from wholesalers, farmers and small distributors at wholesale prices. It also includes a **food-sharing module**: local retailers and bakeries publish products close to their expiry date at a deep discount or for free.

Delivered as:
- a mobile app for families and pool organisers (Flutter);
- a web portal for suppliers, retailers and administrators (React);
- a backend with REST API (Java, Spring Boot).

### 1.1 Project objectives (from DIP-2)

| # | Objective (DIP-2, section 1.4) | Requirements | Verification (DIP-15) |
|---|---|---|---|
| O1 | Reduce the cost of an SSFP basket for pool participants by **at least 15%** compared with the average district retail price | FR-06, FR-07, FR-12, FR-35 | Savings evaluation on three test baskets (9.4) |
| O2 | A new user can create or join a pool in **no more than 3 minutes** | FR-09, FR-11, NFR-08 | Timed usability test, ≥ 80% success (9.3) |
| O3 | **100% correct** share and total calculations in all test scenarios | FR-12, FR-34, NFR-07 | Unit tests T1–T7 (9.2) |
| O4 | Fully bilingual interface in **Kazakh and Russian** | NFR-01 | Manual review, 0 untranslated strings (9.1) |

### 1.2 In scope (MVP, from DIP-2 section 1.5)
Family registration and district/building selection; supplier catalogue with wholesale prices and minimum order quantities; pool creation and joining with automatic share calculation and automatic closure when the target is reached; QR payment per family (Kaspi in sandbox mode); combined order to the supplier; map of pick-up points; food-sharing module; supplier web portal; "social family" status with manual verification; baseline demand forecast for SSFP by district.

### 1.3 Out of scope (from DIP-2)
- In-house delivery service and warehousing. Suppliers deliver the combined order to the pick-up point.
- Live integration with government databases (TSA, eGov). Replaced by document upload and manual verification (FR-04).
- Real payment processing. Kaspi QR works in a sandbox / test environment only.
- Sale of alcohol, tobacco and medicines.
- Multi-city launch. The pilot covers one district of Astana.

---

## 2. Actors

Actor names are the same in the proposal (DIP-2), the use case diagram (DIP-10) and the context diagram (DIP-9).

| Actor | Description | Client |
|---|---|---|
| **Family** | Household member (large family, low-income household, TSA recipient or other resident) who joins pools, pays a share and reserves surplus food | Mobile app |
| **Pool Organiser** | Building representative, head of the condominium association (OSI/KSK) or active resident. A Pool Organiser is also a Family. Creates pools and, in the MVP, acts as the pick-up point and confirms the hand-over of orders | Mobile app |
| **Supplier** | Farmer, wholesaler or small distributor. Publishes the catalogue and fulfils combined orders | Web portal |
| **Retailer / Bakery** | Local shop or bakery that publishes near-expiry products | Web portal |
| **Administrator** | Platform team member. Approves suppliers and retailers, verifies social status, manages pick-up points | Web portal |
| *External:* Kaspi QR | Generates payment QR codes and confirms payments (sandbox) | — |
| *External:* Maps service | 2GIS (Google Maps as fallback). Shows pools and pick-up points | — |
| *External:* Notification service | Firebase: push notifications and SMS login codes | — |

---

## 3. Priority scale (MoSCoW)

- **M (Must):** without it, the project objectives are not achieved. Required for the final defence.
- **S (Should):** important, planned, but the system works without it.
- **C (Could):** desirable if time allows.
- **W (Won't, this time):** consciously excluded from the diploma scope.

---

## 4. Functional requirements

The *Source* column shows where the requirement comes from: DIP-2 scope item, DIP-4 finding ("Implications for requirements"), DIP-6 criterion (C1–C9) or a feature adopted from an existing system (S1–S5).

### 4.1 Accounts and profiles

| ID | Requirement | Priority | Source | Acceptance criteria |
|---|---|---|---|---|
| FR-01 | Families and Pool Organisers log in to the mobile app with a phone number and a one-time SMS code. Suppliers, Retailers and Administrators log in to the web portal with e-mail and password | M | DIP-2 scope | A new user receives a code, enters it and gets access. 3 wrong codes block attempts for 5 minutes. Portal login works with e-mail and password |
| FR-02 | The user selects a role at registration (Family, Supplier, Retailer / Bakery). Supplier and Retailer accounts are activated by an Administrator | M | DIP-2 scope | A Supplier account cannot publish products until its status is "Approved" |
| FR-03 | A family selects its district and building at registration and specifies the number of family members | M | DIP-2 scope, UC "Register and select district" | The profile is saved, and the district is used to show nearby pools |
| FR-04 | A family can apply for "social family" status (TSA recipient, large family) by uploading a supporting document. An Administrator approves or rejects the application | M | DIP-2 scope, DIP-4, DIP-6 C6 | After approval, the profile shows the status badge and the family gets the benefits in FR-26 and FR-34. A rejected application shows the reason |
| FR-05 | Automatic status verification through state databases (eGov, TSA) | W | DIP-2 out of scope | — |

### 4.2 Supplier catalogue

| ID | Requirement | Priority | Source | Acceptance criteria |
|---|---|---|---|---|
| FR-06 | A Supplier publishes products with name, category, unit, wholesale price, minimum order quantity and available quantity | M | DIP-2 scope, DIP-6 C5 | The product appears in the catalogue within 1 minute after saving |
| FR-07 | A Supplier can define tiered prices (the price decreases as the total volume grows) | S | DIP-2 objective O1 | With tiers of 1–49 kg at 300 ₸ and 50+ kg at 250 ₸, a 60 kg pool is calculated at 250 ₸/kg |
| FR-08 | Families search and filter the catalogue by category, price and supplier. SSFP items are marked and shown first | M | DIP-4 ("catalogue prioritising SSFP") | A search for "мука" or "ұн" returns the matching products. The SSFP filter shows only SSFP items |

### 4.3 Purchase pools (core)

| ID | Requirement | Priority | Source | Acceptance criteria |
|---|---|---|---|---|
| FR-09 | A Pool Organiser creates a pool: supplier, products, target quantity (not less than the supplier's minimum order), pick-up point and deadline | M | DIP-2 scope, S3, UC "Create pool" | The pool is created with status "Collecting" and is visible to families in the district |
| FR-10 | Families see nearby pools and pick-up points on a map and in a list | M | DIP-2 scope, DIP-6 C7, UC "Find pick-up point" | Pools within the selected radius (default 2 km) are shown with fill progress. Pick-up points are shown with address and opening hours |
| FR-11 | A family joins a pool by choosing its quantity of each product and paying its share (FR-17) | M | DIP-2 scope, DIP-6 C1, UC "Join pool" | The pool fill progress updates after payment. A family cannot request more than the remaining quantity (DIP-15 T6) |
| FR-12 | The system automatically calculates each family's share: cost of its items at the pool price, minus the social discount if applicable (FR-34) | M | DIP-2 objective O3, DIP-6 C2, UC "Calculate family share" | The sum of all shares equals the supplier order total exactly (0 ₸ difference after rounding). Rounding remainders are assigned to the Pool Organiser's share. DIP-15 tests T1, T2, T4 pass |
| FR-13 | When the target quantity is reached, the pool closes automatically and participants are notified | M | DIP-2 scope | Status changes to "Closed" automatically. A push notification is sent to all participants within 1 minute |
| FR-14 | If the target quantity is not reached by the deadline, the pool is cancelled and all paid shares are refunded (FR-21) | M | DIP-15 T3 | Status "Cancelled". Every paid share gets status "Refunded" |
| FR-15 | A family can leave a pool before it closes. Its payment is refunded | S | DIP-4 (trust) | The family's quantity is returned to the pool, and the refund is recorded |
| FR-16 | Automatic grouping: the system suggests merging small pools for the same supplier and pick-up area, or suggests an existing pool when the user searches for a product | S | S3 | When two pools for the same supplier are within 1 km and both are below target, the Pool Organisers receive a merge suggestion |

### 4.4 Payment and ordering

| ID | Requirement | Priority | Source | Acceptance criteria |
|---|---|---|---|---|
| FR-17 | When a family joins a pool, the system generates a personal Kaspi QR code (sandbox) for its share | M | DIP-2 scope, DIP-4 ("individual QR payment per family"), DIP-6 C3, UC "Pay share by QR" | Each participant receives a unique QR with an amount equal to the share from FR-12 |
| FR-18 | The system tracks the payment status of each participant | M | DIP-6 C3 | After the payment callback (sandbox), the participant's status changes to "Paid" |
| FR-19 | Funds are released to the supplier and a single combined order is generated only when the pool is closed and all shares are paid | M | DIP-4 ("funds released to the supplier only when the pool is complete"), UC "Receive combined order" | The supplier receives one order with total quantities per product, pick-up point and pool ID. No order is created for an incomplete pool |
| FR-20 | If a joined family does not pay within the payment timeout (default 2 hours), its quantity is released back to the pool | S | DIP-4 (trust) | After the timeout, the unpaid quantity is available to other families |
| FR-21 | Refunds for cancelled pools and for families that leave a pool (sandbox) | M | DIP-15 T3 | Every paid share of a cancelled pool gets status "Refunded" |

### 4.5 Pick-up

| ID | Requirement | Priority | Source | Acceptance criteria |
|---|---|---|---|---|
| FR-22 | The Supplier marks the order as delivered to the pick-up point, and participants are notified | M | DIP-2 scope | Participants receive a push "Order ready for pick-up" |
| FR-23 | The Pool Organiser confirms the hand-over by scanning the participant's pick-up QR code | S | UC "Confirm order hand-over" | After scanning, the participant's status changes to "Collected" |

### 4.6 Food-sharing module

| ID | Requirement | Priority | Source | Acceptance criteria |
|---|---|---|---|---|
| FR-24 | A Retailer / Bakery publishes near-expiry products: name, quantity, discounted price (0 for free), expiry date and pick-up window | M | DIP-2 scope, DIP-4, DIP-6 C4, S1, UC "Publish near-expiry product" | The item is visible to families in the district until it is fully reserved or the pick-up window ends |
| FR-25 | A family reserves an item. The reservation expires if the item is not collected within the pick-up window | M | S1, UC "Reserve surplus item" | The reserved quantity is unavailable to others. After the window, the item becomes available again (DIP-15 T7) |
| FR-26 | Families with verified social status get early access to free items (for example, 30 minutes before other users) | S | DIP-6 adopted feature from S5 | During the first 30 minutes, a family without status cannot reserve the item |
| FR-27 | Limit of free reservations per family per day | S | Fair distribution | A family cannot hold more than N active free reservations (N is configurable, default 2) |

### 4.7 Supplier and retailer web portal

| ID | Requirement | Priority | Source | Acceptance criteria |
|---|---|---|---|---|
| FR-28 | The portal shows incoming combined orders and their statuses | M | DIP-2 scope, DIP-6 C9 | The supplier sees the list of orders and can change status to "Confirmed" or "Delivered" |
| FR-29 | The portal shows basic sales statistics (volume by product and by week) | S | DIP-6 C9 | The chart matches the data of completed orders |

### 4.8 Analytics, savings and social discount

| ID | Requirement | Priority | Source | Acceptance criteria |
|---|---|---|---|---|
| FR-30 | Baseline demand forecast for SSFP by district for the next week, shown to Suppliers and Retailers | S | DIP-2 scope, DIP-6 C9, UC "View demand forecast" | The forecast is shown for each product and district. Its error is measured on test data and compared with a naive baseline (last week's demand) |
| FR-31 | Platform report on rescued food (kg) and total family savings (₸) | S | DIP-2 problem statement | The report counts kg from collected food-sharing items and the difference between retail and pool prices |
| FR-34 | A Supplier can set a social discount (%) in a pool for families with verified social status. The discount is applied in the share calculation | S | DIP-4 ("additional discount"), DIP-6 conclusion, DIP-15 T5 | With a 5% social discount, the share of a social family is reduced by 5%, and the totals still match the supplier order (FR-12) |
| FR-35 | Each pool shows the family's savings compared with the average district retail price (BNS SSFP monitoring) | S | DIP-2 objective O1, DIP-4 ("display savings against retail prices") | The pool screen shows retail price, pool price and savings in ₸ and % for each product |
| FR-36 | Participants can rate the Pool Organiser (1–5) after a completed pool | C | DIP-4 ("organiser rating") | The average rating is shown on the Organiser's pools |

### 4.9 Administration

| ID | Requirement | Priority | Source | Acceptance criteria |
|---|---|---|---|---|
| FR-32 | The Administrator approves Suppliers and Retailers and blocks users | M | DIP-2 target users, UC "Moderate suppliers" | A blocked user cannot log in |
| FR-33 | The Administrator manages the list of pick-up points | M | DIP-2 scope | A new pick-up point is available when creating a pool |

---

## 5. Non-functional requirements

| ID | Category | Requirement | Priority | Source | Acceptance criteria / how measured |
|---|---|---|---|---|---|
| NFR-01 | Localisation | The mobile app and the portal fully support Kazakh and Russian, switchable in settings | M | DIP-2 O4, DIP-6 C8 | Manual review of all screens: 0 untranslated strings (DIP-15, 9.1) |
| NFR-02 | Performance | The API responds within 1 second at 100 concurrent requests | M | DIP-15, 9.2 | Load test (k6 or JMeter): 95th percentile ≤ 1 s |
| NFR-03 | Performance | Catalogue and pool list load in the mobile app within 2 s on a 4G connection | S | Usability | Measured on a test device |
| NFR-04 | Security | All traffic uses HTTPS. Authentication uses JWT with expiry. Portal passwords are stored as salted hashes (bcrypt) | M | DIP-15, 9.2 | Configuration and code review. HTTP requests are rejected. No plain-text passwords in the database |
| NFR-05 | Security / Legal | Personal data and social status documents are processed in accordance with the Law of the Republic of Kazakhstan "On Personal Data and Their Protection". Documents are accessible to Administrators only | M | DIP-15, 9.2 | Role-based access test: a Family or Supplier account gets 403 when requesting a document |
| NFR-06 | Reliability | Payment status updates are idempotent: a repeated payment callback does not create a double payment | M | DIP-6 C3 | Automated test: the same callback sent twice changes the status once |
| NFR-07 | Correctness | Share and total calculations are exact to 1 ₸ | M | DIP-2 O3 | 100% of unit test scenarios pass (DIP-15 T1–T7, extended during implementation) |
| NFR-08 | Usability | A new user can create or join a pool within 3 minutes | M | DIP-2 O2 | Timed usability test with 5–8 target users: ≥ 80% succeed (DIP-15, 9.3) |
| NFR-09 | Usability | Readable interface for older users: minimum font 14 sp, contrast per WCAG 2.1 AA | S | Target users | Contrast check of the main screens |
| NFR-10 | Usability | User satisfaction: SUS score ≥ 68 and mean ≥ 4.0 on questionnaire items 1, 4 and 5 | S | DIP-15, 9.3 | Post-test questionnaire |
| NFR-11 | Maintainability | Backend business logic (pools, shares, payments) has at least 60% automated test coverage | S | Quality | Coverage report in CI |
| NFR-12 | Portability | The mobile app runs on Android 8+ and iOS 14+ | S | DIP-2 scope | Build and launch on both platforms |
| NFR-13 | Availability | Target availability of 99% during the pilot and testing | C | Pilot | Uptime monitoring |

---

## 6. Traceability

### 6.1 Requirements → use cases (DIP-10) → components (DIP-11) → verification (DIP-15)

| Use case (DIP-10) | Actor | Requirements | Component (DIP-11) | Verification (DIP-15) |
|---|---|---|---|---|
| UC1 Register and select district | Family | FR-01, FR-03 | Users module | Usability test |
| UC2 Browse catalogue | Family | FR-08 | Catalogue module | Usability test |
| UC3 Join pool | Family | FR-11, FR-15, FR-20 | Pools module | Integration test, usability task 1 |
| UC4 Calculate family share | — | FR-12, FR-34, NFR-07 | Pools module (share calculator) | Unit tests T1–T6 |
| UC5 Pay share by QR | Family, Kaspi QR | FR-17, FR-18, FR-21, NFR-06 | Payments module + Kaspi adapter | Integration test, usability task 2 |
| UC6 Find pick-up point | Family | FR-10 | Pools module, maps | Usability task 3 |
| UC7 Reserve surplus item | Family | FR-25, FR-26, FR-27 | Food-sharing module | Unit test T7, usability task 4 |
| UC8 Apply for social status | Family | FR-04 | Users module, file storage | NFR-05 access test |
| UC9 Create pool | Pool Organiser | FR-09, FR-16 | Pools module | Usability test (NFR-08) |
| UC10 Confirm order hand-over | Pool Organiser | FR-22, FR-23 | Pools module | Integration test |
| UC11 Publish products and wholesale prices | Supplier | FR-06, FR-07 | Catalogue module | Integration test |
| UC12 Receive combined order | Supplier | FR-19, FR-28 | Orders module, portal | Integration test |
| UC13 View demand forecast | Supplier, Retailer / Bakery | FR-30 | Analytics module | Forecast error vs naive baseline |
| UC14 Publish near-expiry product | Retailer / Bakery | FR-24 | Food-sharing module | Integration test |
| UC15 Verify social status | Administrator | FR-04, FR-05 | Admin module | NFR-05 access test |
| UC16 Moderate suppliers | Administrator | FR-02, FR-32 | Admin module | Integration test |

> Not shown as separate use cases in DIP-10: savings display (FR-35), organiser rating (FR-36), pick-up point management (FR-33). They can be added to the diagram or kept as part of UC3, UC10 and UC16.

### 6.2 DIP-6 criteria → requirements

| DIP-6 criterion | Requirements |
|---|---|
| C1 Collective wholesale purchasing (pools) | FR-09 … FR-16 |
| C2 Automatic share calculation | FR-12, NFR-07 |
| C3 Individual payment (Kaspi QR) | FR-17, FR-18, FR-21, NFR-06 |
| C4 Discounted surplus food | FR-24 … FR-27 |
| C5 Direct sourcing from farmers and wholesalers | FR-06, FR-07 |
| C6 Social status support | FR-04, FR-26, FR-34 |
| C7 Map of pick-up points | FR-10, FR-33 |
| C8 Kazakh / Russian interface | NFR-01 |
| C9 Demand forecasting / supplier portal | FR-28, FR-29, FR-30 |

---

## 7. Open questions (to be answered by the interviews, DIP-4)

| # | Question | Interview guide question (DIP-4) | Affects |
|---|---|---|---|
| 1 | Who usually takes the Pool Organiser role: an active resident, the building representative or OSI/KSK? | R3 guide | FR-09, FR-23 |
| 2 | Is it acceptable to pay when joining a pool (with refund if the pool is cancelled)? What payment timeout is acceptable? | Families Q7, Q9 | FR-17, FR-20, FR-21 |
| 3 | What minimum order quantities and price tiers do suppliers actually use for flour, potatoes, oil and sugar? | R4 guide | FR-06, FR-07, O1 |
| 4 | Are retailers ready to list near-expiry products daily, two to three hours before closing? | R5 guide | FR-24, FR-25 |
| 5 | Which pick-up location is most convenient? | Families Q11, R3 guide | FR-10, FR-33 |
| 6 | Which document is acceptable to confirm social status? Would suppliers give an additional social discount? | Families Q3, R4 guide | FR-04, FR-34 |

---

## 8. Summary

| Priority | Functional | Non-functional |
|---|---|---|
| Must | 22 | 7 |
| Should | 12 | 5 |
| Could | 1 | 1 |
| Won't | 1 | 0 |
| **Total** | **36** | **13** |

---

## 9. Change log

| Version | Change | Reason |
|---|---|---|
| v0.1 | Initial draft | — |
| v0.2 | Actors renamed to match DIP-2 and DIP-10 ("Pool Organiser", "Retailer / Bakery"); the Pool Organiser acts as the pick-up point | Consistency with proposal and use case diagram |
| v0.2 | Payment moved to the moment of joining; funds released to the supplier only when the pool is complete; refunds for cancelled pools became Must | DIP-4 finding on trust, DIP-10 (Join pool includes Pay share), DIP-15 T3 |
| v0.2 | Social status (FR-04) raised to Must; added social discount (FR-34) | DIP-2 scope, DIP-4, DIP-15 T5 |
| v0.2 | Demand forecast (FR-30) raised from Could to Should | DIP-2 includes the baseline forecast in the MVP scope |
| v0.2 | Added savings display (FR-35) and organiser rating (FR-36) | DIP-2 objective O1, DIP-4 |
| v0.2 | NFR-02 changed to 1 s at 100 concurrent requests; NFR-08 changed to "within 3 minutes, ≥ 80%"; added NFR-10 (SUS); NFR-04 covers portal passwords | Consistency with DIP-2 objectives and DIP-15 |
| v0.2 | Out of scope extended (alcohol, tobacco, medicines; one pilot district in Astana); added objectives, sources and traceability to DIP-6 and DIP-10 | DIP-2, DIP-6, DIP-10 |
