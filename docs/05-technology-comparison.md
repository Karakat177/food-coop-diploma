# Technology Comparison

**Project:** Information system for optimizing collective food purchasing and food redistribution
**Task:** DIP-7 · **Owner:** Student B · **Status:** Draft v0.3
**Depends on:** Requirements specification (`06-requirements.md`, DIP-8), Existing systems comparison (`04-existing-systems-comparison.md`, DIP-6)

---

## 1. Method

For each key technical decision we compare 2–3 realistic alternatives against criteria derived from the project requirements. Each criterion is linked to the requirement IDs it comes from.

Scores are the team's assessment on a 1–5 scale (5 = best fit for this project), based on official documentation and the constraints of a diploma project: a team of 3, about one academic year, limited budget, demonstration rather than production load.

Weights reflect how important a criterion is for this project (total = 100%). The weighted score is `Σ (score × weight)`.

### Project constraints that drive the choices

| Constraint | Source |
|---|---|
| Money must be split exactly between families and match the supplier order total | FR-12, NFR-07 |
| Payment status must be reliable and idempotent | FR-17 … FR-19, NFR-06 |
| Pools and food items are searched by distance ("within 2 km") | FR-10, FR-16, FR-24 |
| One mobile app for Android and iOS, Kazakh and Russian UI | NFR-01, NFR-12 |
| Time-based events: pool deadlines, reservation expiry, notifications | FR-13, FR-14, FR-25 |
| Small team, fixed deadline: technologies must be known to the team and well documented | Project scope |

### Lessons from existing systems (DIP-6)

The existing systems comparison (`04-existing-systems-comparison.md`) shows which features we adopt and what limits current solutions. These findings affect the technical choices below.

| Finding in DIP-6 | System | Technical consequence | Decision |
|---|---|---|---|
| Group buying works through a resident leader, one combined order and one pickup point | S3 China community group buying | The core data model is pool → participants → shares → one supplier order. All steps must be consistent | Decision 1 (single transaction in a modular monolith), Decision 3 (relational DB) |
| Chinese platforms depend on the WeChat ecosystem and WeChat Pay | S3 | Payment must use the dominant local method. In Kazakhstan this is Kaspi, so families need no new wallet. The payment provider is hidden behind an adapter so the platform is not tied to one ecosystem | Decision 6 (Kaspi QR via adapter) |
| Joint purchases in Kazakhstan are organised manually in messenger groups, with prepayment to one person and disputes | DIP-6 conclusion 2 | A messenger bot was considered as the client, but a standalone app is needed for maps, QR scanning, payment per participant and a readable UI. Automatic share calculation removes disputes | Decision 4 (Flutter app), FR-12 |
| Surplus food is listed with a limited collection window | S1 Too Good To Go | Reservations must expire automatically at an exact time | Decision 5.2 (scheduled jobs with Quartz) |
| Offers are shown on a map of nearby listings | S1, S2 OLIO | Indexed distance queries are needed | Decision 3 (PostGIS), Decision 6 (2GIS) |
| Priority for vulnerable families exists only offline | S5 Food Bank | Status documents must be stored securely with access only for moderators | Decision 3 (object storage with restricted access), NFR-05 |
| No system offers Kazakh and Russian together with these functions | S1–S3 | Full localisation from the start | Decision 4 (Flutter i18n), NFR-01 |
| Demand forecasting is used by large platforms | S3 | The proposal (DIP-2) includes a baseline forecast in the MVP, but it is not part of the core purchasing flow | Separate offline Python script (FR-30, priority Should) |

---

## 2. Decision 1: Architectural style

| Criterion (weight) | Linked req. | Modular monolith | Microservices | Serverless functions (BaaS) |
|---|---|---|---|---|
| Development speed for a team of 3 (25%) | Scope | 5 | 2 | 4 |
| Transactional consistency of pools and payments (25%) | FR-12, NFR-06 | 5 | 2 | 3 |
| Ease of deployment and debugging (20%) | NFR-10 | 5 | 2 | 3 |
| Ability to separate modules later (15%) | NFR-11 | 4 | 5 | 3 |
| Control over business logic and testability (15%) | NFR-07, NFR-11 | 5 | 4 | 2 |
| **Weighted score** | | **4.85** | **2.75** | **3.10** |

**Choice: modular monolith.** One deployable backend split into clear modules (Users, Catalog, Pools, Payments, Food-sharing, Notifications, Analytics) with separate packages, interfaces and database schemas.

**Justification:**
- The core operation (joining a pool → recalculating shares → generating payments) touches several modules and must be consistent. Inside one application this is a single database transaction. With microservices it would require distributed transactions or sagas, which add complexity without benefit at our scale.
- Microservices bring their own infrastructure costs (service discovery, per-service deployment, network failures between services, distributed tracing). These are justified for large teams and high load, which this project does not have.
- Module boundaries are defined from the start and checked automatically (Spring Modulith, see Decision 2), so a module such as Analytics can be extracted into a separate service later if needed.

---

## 3. Decision 2: Backend platform

| Criterion (weight) | Linked req. | Java + Spring Boot | Node.js + NestJS (TypeScript) | Go (Gin / Echo) |
|---|---|---|---|---|
| Team familiarity and learning curve (25%) | Scope | 5 | 3 | 2 |
| Transactions and exact money calculation (20%) | FR-12, NFR-06, NFR-07 | 5 | 3 | 4 |
| Structure for a modular monolith (15%) | Decision 1 | 5 | 5 | 3 |
| Libraries: ORM, security/JWT, validation, OpenAPI (15%) | NFR-04, NFR-11 | 5 | 5 | 4 |
| Development speed (amount of boilerplate) (15%) | Scope | 3 | 5 | 3 |
| Performance for target load: ≤ 1 s at 100 concurrent requests (10%) | NFR-02 | 4 | 4 | 5 |
| **Weighted score** | | **4.60** | **4.00** | **3.30** |

**Choice: Java 21 with Spring Boot 3.**

**Justification:**
- **Team experience.** The team studied Java during the university program, so it carries the lowest learning risk under a fixed deadline.
- **Money and transactions.** `BigDecimal` provides exact decimal arithmetic for share calculation, with explicit rounding modes (FR-12, NFR-07). Spring's declarative transactions (`@Transactional`) make "join pool → recalculate shares → create payments" a single atomic operation (NFR-06). In JavaScript, numbers are floating-point by default, so exact money handling requires extra discipline or libraries.
- **Modular monolith.** Spring Modulith lets us declare application modules and verify in tests that modules do not access each other's internals. This directly supports Decision 1.
- **Ecosystem.** Spring Data JPA (with Hibernate Spatial for PostGIS), Spring Security (JWT), Bean Validation, springdoc-openapi (Swagger) and Testcontainers for integration tests with a real PostgreSQL.
- **Trade-off.** Spring Boot needs more code and configuration than NestJS, and the backend no longer shares a language with the React web portal. This is mitigated by generating a TypeScript API client from the OpenAPI specification.

> Assumption to confirm: all team members are comfortable with Java. If not, NestJS remains the main alternative.

**Forecasting (FR-30, priority Should)** is implemented as a separate offline Python script (pandas, statsmodels or Prophet). It reads data from PostgreSQL and writes forecasts back, so it does not affect the backend language choice.

---

## 4. Decision 3: Data storage

| Criterion (weight) | Linked req. | PostgreSQL (+ PostGIS) | MongoDB | MySQL |
|---|---|---|---|---|
| ACID transactions for money and payment statuses (30%) | FR-12, FR-18, NFR-06 | 5 | 3 | 5 |
| Geospatial queries ("pools within 2 km") (20%) | FR-10, FR-16, FR-24 | 5 | 4 | 3 |
| Relational data model: families ↔ pools ↔ products ↔ payments (20%) | FR-09 … FR-19 | 5 | 2 | 5 |
| Constraints and integrity (foreign keys, CHECK) (15%) | NFR-07 | 5 | 2 | 4 |
| Support for analytics queries (aggregations by district, week) (15%) | FR-29, FR-31 | 5 | 4 | 4 |
| **Weighted score** | | **5.00** | **3.00** | **4.30** |

**Choice: PostgreSQL with the PostGIS extension.**

**Justification:**
- The data is strongly relational: a pool has participants, each participant has items and a payment, each payment belongs to a supplier order. Foreign keys and constraints protect these links.
- Money and payment statuses require transactions. MongoDB supports multi-document transactions, but the document model is a weaker fit for many-to-many links between families, pools and products.
- PostGIS provides indexed distance queries for "pools and food items near me". In Java it is accessed through Hibernate Spatial.
- Amounts are stored as `NUMERIC` in the database and `BigDecimal` in Java, never as floating-point numbers (NFR-07).
- Schema changes are versioned with Flyway migrations stored in the repository.

**Supporting storage:** uploaded social status documents are stored in S3-compatible object storage (MinIO locally), with access only for Moderators (NFR-05).

---

## 5. Decision 4: Mobile application

| Criterion (weight) | Linked req. | Flutter | React Native | Native (SwiftUI + Kotlin) |
|---|---|---|---|---|
| One codebase for Android and iOS (25%) | NFR-12 | 5 | 5 | 1 |
| Development speed for a team of 3 (20%) | Scope | 4 | 4 | 2 |
| Localization (Kazakh, Russian) (15%) | NFR-01 | 5 | 4 | 5 |
| Map and QR code support (plugins) (15%) | FR-10, FR-17, FR-23 | 4 | 4 | 5 |
| UI consistency across devices, readable for older users (15%) | NFR-09 | 5 | 4 | 5 |
| Shared code with the web portal (10%) | FR-28 | 2 | 4 | 1 |
| **Weighted score** | | **4.35** | **4.25** | **3.00** |

**Choice: Flutter (Dart).**

**Justification:**
- One codebase covers Android and iOS, which is critical for a team of 3. Native development would double the work.
- Flutter has built-in internationalization (`intl`, ARB files) for Kazakh and Russian, and draws its own UI, so screens look the same on all devices. This helps meet readability requirements for older users.
- Dart's syntax (classes, static typing) is close to Java, so the team can switch between backend and mobile code easily.
- React Native is a close alternative. Its advantage (sharing code with a React web portal) is smaller than Flutter's advantages in UI consistency for this project.

**Web portal for suppliers and partners:** React + TypeScript. It is a separate, simpler application (tables, forms, charts). Its API client is generated from the backend's OpenAPI specification.

---

## 6. Decision 5: Component interaction

### 6.1 Client ↔ server API

| Criterion (weight) | Linked req. | REST (JSON + OpenAPI) | GraphQL | gRPC |
|---|---|---|---|---|
| Simplicity for the team and for testing (30%) | NFR-11 | 5 | 3 | 2 |
| Support in Flutter and in the browser (25%) | NFR-12 | 5 | 4 | 2 |
| Compatibility with payment callbacks (webhooks) (20%) | FR-18 | 5 | 2 | 2 |
| Documentation and contract (20%) | NFR-11 | 5 | 4 | 4 |
| Flexible queries for different screens (5%) | FR-08 | 3 | 5 | 3 |
| **Weighted score** | | **4.90** | **3.35** | **2.45** |

**Choice: REST API with OpenAPI (Swagger) documentation.** springdoc-openapi generates the specification from the Spring controllers. It also serves as the API example for the UX/prototype section (DIP-14). Payment systems call back using HTTP webhooks, which fit REST naturally.

### 6.2 Background tasks and events

| Criterion (weight) | Linked req. | Quartz Scheduler (JDBC store in PostgreSQL) | Message broker (RabbitMQ / Kafka) | Simple polling (`@Scheduled`) |
|---|---|---|---|---|
| Delayed jobs: pool deadlines, reservation expiry (30%) | FR-14, FR-25 | 5 | 3 | 3 |
| Retries for notifications and payment checks (25%) | FR-13, NFR-06 | 4 | 5 | 2 |
| Infrastructure complexity (25%) | Scope | 5 | 2 | 5 |
| Fit with a monolith (20%) | Decision 1 | 5 | 3 | 4 |
| **Weighted score** | | **4.75** | **3.25** | **3.45** |

**Choice: Quartz Scheduler with a JDBC job store**, integrated through Spring Boot. A job such as "cancel the pool if it is not filled by the deadline" is scheduled for an exact time and stored in PostgreSQL, so it survives an application restart. No extra infrastructure is needed. Inside the application, modules communicate through Spring application events (for example, `PoolFilledEvent` → Notifications module). A message broker such as Kafka is designed for event streaming between many services and is unnecessary for a monolith.

---

## 7. Decision 6: External services

| Service | Alternatives considered | Choice | Reason |
|---|---|---|---|
| Payments | Kaspi QR, Halyk ePay, international providers (Stripe) | **Kaspi QR via an adapter, sandbox (test environment) in the MVP** | Kaspi is the most widely used payment app in Kazakhstan, so families already have it. This follows the lesson from S3 in DIP-6: group buying succeeds when it uses the payment method people already have (WeChat Pay in China). Real payment processing is out of scope (DIP-2) and merchant access requires a registered legal entity, so the MVP uses the sandbox behind the same interface (FR-17). The adapter allows Halyk to be added later |
| Maps | 2GIS, Google Maps, Yandex Maps | **2GIS** (alternative: Google Maps) | Detailed data on Kazakhstani cities, including buildings and entrances, which matters for pickup points in residential buildings. To be confirmed after checking SDK terms and access for students |
| Push notifications | Firebase Cloud Messaging, OneSignal | **Firebase Cloud Messaging** | Free, works for both Android and iOS, official Flutter plugin and Java Admin SDK |
| SMS codes | Local SMS providers, Firebase Phone Auth | **Firebase Phone Auth for the MVP** | Avoids contracting an SMS provider during the diploma. Can be replaced with a local provider later |

---

## 8. Resulting technology stack

| Layer | Technology | Language |
|---|---|---|
| Mobile app (families) | Flutter | Dart |
| Web portal (suppliers, partners, admin) | React | TypeScript |
| Backend | Spring Boot 3, Spring Modulith, modular monolith | Java 21 |
| Data access | Spring Data JPA, Hibernate Spatial, Flyway | Java / SQL |
| API | REST + OpenAPI (springdoc-openapi) | — |
| Database | PostgreSQL + PostGIS | SQL |
| Background jobs | Quartz Scheduler (JDBC store), Spring events | Java |
| File storage | S3-compatible object storage (MinIO locally) | — |
| Baseline forecasting (FR-30, Should) | Offline script (pandas, statsmodels or Prophet) | Python |
| External | Kaspi QR (sandbox, via adapter), 2GIS, Firebase (FCM, Phone Auth) | — |
| Build and tests | Gradle, JUnit 5, Testcontainers, JaCoCo (coverage, NFR-11) | — |
| Deployment and CI | Docker, Docker Compose, GitHub Actions | — |

---

## 9. Risks of the chosen technologies

| Risk | Mitigation |
|---|---|
| Spring Boot requires a lot of configuration at the start | Generate the project with Spring Initializr. Build a small vertical slice (log in → view pools) in the first two weeks of implementation |
| The team has no experience with Flutter | Dart is close to Java. Start with one screen and the API client before building all screens |
| Backend (Java) and web portal (TypeScript) use different languages | Generate the TypeScript API client from the OpenAPI specification |
| Kaspi API access is not available to students | If the official sandbox is not available, a local stub with the same PaymentProvider interface is used. Real payments are out of scope (DIP-2) |
| 2GIS SDK licensing restrictions | Google Maps as a fallback. Map logic is hidden behind one widget |
| The monolith grows too large | Spring Modulith verification tests for module boundaries, code review in Pull Requests |

---

## 10. References

- Spring Boot documentation: https://docs.spring.io/spring-boot/
- Spring Modulith documentation: https://docs.spring.io/spring-modulith/reference/
- Spring Framework — Transaction management: https://docs.spring.io/spring-framework/reference/data-access/transaction.html
- Java SE `BigDecimal`: https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/math/BigDecimal.html
- springdoc-openapi: https://springdoc.org/
- Quartz Scheduler documentation: https://www.quartz-scheduler.org/documentation/
- PostgreSQL documentation — Transactions: https://www.postgresql.org/docs/current/tutorial-transactions.html
- PostGIS documentation: https://postgis.net/documentation/
- Flutter documentation — Internationalization: https://docs.flutter.dev/ui/accessibility-and-internationalization/internationalization
- OpenAPI Specification: https://spec.openapis.org/oas/latest.html
- Fowler, M. "MonolithFirst": https://martinfowler.com/bliki/MonolithFirst.html
