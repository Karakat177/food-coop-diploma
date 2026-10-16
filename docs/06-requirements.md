# Requirements Specification

**Project:** Information system for optimizing collective food purchasing and food redistribution
**Task:** DIP-8 · **Owner:** Student B · **Status:** Draft v0.1 (to be refined after interviews, DIP-4)

---

## 1. Purpose and scope

The system lets families living in the same district or building join **purchase pools** and buy socially significant food products (SZPT) directly from wholesalers, farmers and small distributors at wholesale prices. It also includes a **food-sharing module**: local supermarkets and bakeries publish products close to their expiry date for free or at a deep discount.

Delivered as:
- a mobile app for families (Flutter);
- a web portal for suppliers and food-sharing partners;
- a backend with REST API.

### 1.1 In scope for the diploma (MVP)
Pools, share calculation, split payment via QR, single consolidated supplier order, pickup points, food-sharing listings, supplier portal, Kazakh/Russian UI, basic demand analytics.

### 1.2 Out of scope (explicitly)
- Real integration with state databases (eGov) for low-income status verification. In the MVP, it is replaced by a document upload and manual moderation.
- Own delivery logistics (couriers). Goods are collected at pickup points.
- Live payments with real money. The Kaspi integration is implemented against a sandbox or mock, because merchant API access requires a registered legal entity.

> Assumption to verify: suppliers are willing to accept a single consolidated order and payment collected from several families (DIP-4 interviews).

---

## 2. Stakeholders and actors

| Actor | Description |
|---|---|
| **Family (Participant)** | Household member who joins pools and claims food-sharing items |
| **Pool Organizer** | Family member or building representative who creates a pool and confirms pickup |
| **Supplier** | Wholesaler, farmer or distributor who publishes a catalog and fulfills consolidated orders |
| **Food-sharing Partner** | Supermarket, bakery or canteen that publishes surplus or near-expiry products |
| **Pickup Point Operator** | KSK/OSI, building representative or partner shop where orders are collected |
| **Administrator / Moderator** | Manages users, verifies social status documents, resolves disputes |
| *External:* Payment system | Kaspi QR (sandbox or mock), generates payment links and confirms payments |
| *External:* Maps service | 2GIS or Google Maps, used to show pools and pickup points |
| *External:* Notification service | Push (Firebase Cloud Messaging) and SMS for verification codes |

---

## 3. Priority scale (MoSCoW)

- **M (Must):** without it, the project aim is not achieved. Required for the final defense.
- **S (Should):** important, planned, but the system works without it.
- **C (Could):** desirable if time allows.
- **W (Won't, this time):** consciously excluded from the diploma scope.

---

## 4. Functional requirements

### 4.1 Accounts and profiles

| ID | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| FR-01 | Users register and log in with a phone number and a one-time SMS code | M | A new user receives a code, enters it and gets access. A wrong code 3 times blocks attempts for 5 minutes |
| FR-02 | The user selects a role at registration (Family, Supplier, Food-sharing Partner). Supplier and Partner accounts are activated by an Administrator | M | A Supplier account cannot publish products until its status is "Approved" |
| FR-03 | A family profile stores the address (district/building) and the number of family members | M | The profile is saved, and the address is used to show nearby pools |
| FR-04 | A family can request "socially vulnerable" status by uploading a supporting document. A Moderator approves or rejects the request | S | After approval, the profile shows the status badge, and the family gets priority access to food-sharing items (FR-24) |
| FR-05 | Status verification through state databases (eGov) | W | — |

### 4.2 Supplier catalog

| ID | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| FR-06 | A Supplier publishes products with name, category, unit, wholesale price, minimum batch and available quantity | M | The product appears in the catalog within 1 minute after saving |
| FR-07 | A Supplier can define tiered prices (the price decreases as the total volume grows) | S | With tiers of 1–49 kg at 300 ₸ and 50+ kg at 250 ₸, a 60 kg pool is calculated at 250 ₸/kg |
| FR-08 | Families search and filter the catalog by category, price and supplier, and SZPT products are marked | M | A search for "мука" or "ұн" returns the matching products. The SZPT filter shows only SZPT items |

### 4.3 Purchase pools (core)

| ID | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| FR-09 | An Organizer creates a pool: supplier, products, total target quantity, pickup point and collection deadline | M | The pool is created with status "Collecting" and is visible to families within the configured radius |
| FR-10 | Families see nearby pools on a map and in a list | M | Pools within the selected radius (default 2 km) are displayed with their fill progress |
| FR-11 | A family joins a pool by choosing its quantity of each product | M | The pool's fill progress updates immediately. A family cannot request more than the remaining quantity |
| FR-12 | The system automatically calculates each family's share: cost of its items + proportional part of shared costs (for example, delivery to the pickup point) | M | The sum of all shares equals the supplier order total exactly (difference 0 ₸ after rounding). Rounding remainders are assigned to the Organizer's share |
| FR-13 | When the pool reaches the supplier's minimum batch, its status changes to "Ready for payment" and participants are notified | M | Status changes automatically, and a push notification is sent to all participants within 1 minute |
| FR-14 | If the minimum batch is not reached by the deadline, the pool is cancelled and participants are notified | M | Status "Cancelled". No payment requests remain active |
| FR-15 | A family can leave a pool before payment | S | The family's quantity is returned to the pool, and shares are recalculated |
| FR-16 | Automatic grouping: the system suggests merging small pools for the same supplier and pickup area, or suggests an existing pool when the user searches for a product | S | When two pools for the same supplier are within 1 km and each is below the minimum, the Organizers receive a merge suggestion |

### 4.4 Payment and ordering

| ID | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| FR-17 | The system generates a personal payment QR code (Kaspi QR, sandbox or mock) for each family's share | M | Each participant receives a unique QR with an amount equal to their share from FR-12 |
| FR-18 | The system tracks the payment status of each participant | M | After the payment callback (or mock confirmation), the participant's status changes to "Paid" |
| FR-19 | When all shares are paid, the system generates a single consolidated order for the supplier | M | The supplier receives one order with total quantities per product, pickup point and pool ID |
| FR-20 | Unpaid shares: after the payment deadline, the Organizer can remove the unpaid participant or cover the share | S | The pool can proceed to ordering once all remaining shares are paid |
| FR-21 | Refund for a cancelled pool after payment | C | Refund is initiated for all paid participants |

### 4.5 Pickup

| ID | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| FR-22 | The Supplier marks the order as delivered to the pickup point, and participants are notified | M | Participants receive a push "Order ready for pickup" |
| FR-23 | A participant confirms pickup by showing a pickup QR code to the Pickup Point Operator or Organizer | S | After scanning, the participant's status changes to "Collected" |

### 4.6 Food-sharing module

| ID | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| FR-24 | A Partner publishes surplus items: name, quantity, price (0 for free), expiry date and pickup window | M | The item is visible to families within the radius until it is fully claimed or the pickup window ends |
| FR-25 | A family reserves an item, and the reservation expires if not collected within the pickup window | M | The reserved quantity is unavailable to others. After the window, the reservation is cancelled automatically |
| FR-26 | Families with verified social status get early access to free items (for example, 30 minutes before other users) | S | During the first 30 minutes, a family without status cannot reserve the item |
| FR-27 | Limit of free reservations per family per day | S | A family cannot hold more than N active free reservations (N is configurable, default 2) |

### 4.7 Supplier and partner web portal

| ID | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| FR-28 | The portal shows incoming consolidated orders and their statuses | M | The supplier sees the list of orders and can change status to "Confirmed" or "Delivered" |
| FR-29 | The portal shows basic sales statistics (volume by product and by week) | S | The chart matches the data of completed orders |

### 4.8 Analytics and AI

| ID | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| FR-30 | Demand forecast for SZPT products by district for the next week, shown to suppliers | C | The forecast is shown for each product and district. Its error is measured on test data (see the evaluation plan, DIP-15) |
| FR-31 | Report on rescued food (kg) and family savings (₸) for the platform | S | The report counts kg from collected food-sharing items and the difference between retail and pool prices |

### 4.9 Administration

| ID | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| FR-32 | The Administrator approves suppliers and partners and blocks users | M | A blocked user cannot log in |
| FR-33 | The Administrator manages the list of pickup points | M | A new pickup point is available for selection when creating a pool |

---

## 5. Non-functional requirements

| ID | Category | Requirement | Priority | Acceptance criteria / how measured |
|---|---|---|---|---|
| NFR-01 | Localization | The mobile app and portal fully support Kazakh and Russian, switchable in settings | M | All UI screens have no untranslated strings in either language (manual checklist) |
| NFR-02 | Performance | API responds to 95% of requests within 500 ms at 100 concurrent users | M | Load test (k6 or JMeter), p95 ≤ 500 ms |
| NFR-03 | Performance | Catalog and pool list load on the mobile app within 2 s on a 4G connection | S | Measured on a test device |
| NFR-04 | Security | Passwords and tokens are not stored in plain text. All traffic uses HTTPS. Authentication uses JWT with expiry | M | Code review and configuration check. HTTP requests are rejected |
| NFR-05 | Security / Legal | Personal data and social status documents are processed in accordance with the Law of the Republic of Kazakhstan "On Personal Data and Their Protection". Documents are accessible only to Moderators | M | Role-based access test: a Family or Supplier account gets 403 when requesting a document |
| NFR-06 | Reliability | Payment status updates are idempotent: a repeated payment callback does not create a double payment | M | Automated test: the same callback sent twice changes the status once |
| NFR-07 | Correctness | Share calculation is exact to 1 ₸ with no loss on rounding | M | Unit tests on at least 20 pool scenarios, sum of shares = order total |
| NFR-08 | Usability | A first-time user can join an existing pool in no more than 5 steps (taps) from the main screen | S | Usability test with 5 users (DIP-15) |
| NFR-09 | Usability | Interface readable for older users: minimum font 14 sp, contrast per WCAG 2.1 AA | S | Contrast check of the main screens |
| NFR-10 | Availability | Target availability of 99% during demonstration and testing | C | Uptime monitoring |
| NFR-11 | Maintainability | Backend code has automated tests with at least 60% coverage of the business logic (pools, shares, payments) | S | Coverage report in CI |
| NFR-12 | Portability | The mobile app runs on Android 8+ and iOS 14+ | S | Build and launch on both platforms |

---

## 6. Traceability

| Requirement group | Use case (DIP-10) | Component (DIP-11) | Verification (DIP-15) |
|---|---|---|---|
| FR-09 … FR-16 | Create pool, Join pool | Pool Service | Unit + integration tests, pool scenarios |
| FR-12, NFR-07 | Calculate shares | Pool Service (share calculator) | Unit tests on 20+ scenarios |
| FR-17 … FR-21, NFR-06 | Pay share | Payment Service + Kaspi adapter | Integration tests with mock |
| FR-24 … FR-27 | Publish / reserve surplus food | Food-sharing Service | Integration tests |
| FR-30 | View demand forecast | Analytics Service | Forecast error on test data |
| NFR-01, NFR-08 | All family scenarios | Mobile App | Usability test |

> Use case and component names will be updated when DIP-10 and DIP-11 are completed.

---

## 7. Open questions (to be resolved with DIP-4 interviews and the supervisor)

1. Who usually takes the Organizer role: an active resident, the building representative or the KSK/OSI?
2. Which shared costs exist in practice (delivery, packaging), and how should they be split: equally or by weight/cost?
3. What minimum batches and price tiers do suppliers actually use for flour, potatoes, oil, sugar?
4. Are supermarkets and bakeries ready to publish surplus items daily, and at what time?
5. Which document is acceptable to confirm "socially vulnerable" status (for example, a certificate of receiving targeted social assistance, or of being a large family)?
6. What is the acceptable payment deadline for participants before a pool is cancelled?

---

## 8. Summary

| Priority | Functional | Non-functional |
|---|---|---|
| Must | 20 | 6 |
| Should | 10 | 5 |
| Could | 2 | 1 |
| Won't | 1 | 0 |
