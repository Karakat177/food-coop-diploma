# 9. Verification and Evaluation Plan

## 9.1 Evaluation Targets

| Objective | Method | Success criterion |
|-----------|--------|-------------------|
| Savings of at least 15% | Compare pool basket price with average district retail price | Savings ≥ 15% on three test baskets |
| Create or join a pool within 3 minutes | Timed usability test | ≥ 80% of participants succeed |
| Correct share calculation | Unit tests of the allocation algorithm | 100% of tests pass |
| Bilingual interface | Manual review of all screens in Kazakh and Russian | 0 untranslated strings |

## 9.2 Verification

### Unit Tests: Share Allocation Algorithm

| ID | Scenario | Input | Expected result |
|----|----------|-------|-----------------|
| T1 | Equal split | 50 kg bag at KZT 15,000; 5 families × 10 kg | KZT 3,000 each |
| T2 | Unequal shares | 50 kg: 20 + 15 + 10 + 5 kg | KZT 6,000 / 4,500 / 3,000 / 1,500 |
| T3 | Pool not filled | 40 of 50 kg committed by deadline | Pool cancelled; payments refunded |
| T4 | Rounding | KZT 10,000 across 3 families | Sum of shares equals KZT 10,000 |
| T5 | Social discount | Family with social status, 5% discount | Share reduced according to pool rules |
| T6 | Over-commitment | Request exceeds remaining quantity | Only remaining quantity offered |
| T7 | Expired reservation | Food-sharing item not collected in window | Item becomes available again |

### Integration Test

Create pool → three families join → QR codes generated (sandbox) → pool closes → order appears in the supplier portal.

### Non-Functional Tests

- API response time under 1 second at 100 concurrent requests
- Passwords stored as salted hashes
- Social status documents accessible to administrators only

## 9.3 Validation

### Usability Test

- **Participants:** 5–8 members of the target group.
- **Tasks:**
  1. Find a flour pool for your building and join it.
  2. Pay your share by QR code.
  3. Find your pick-up point.
  4. Reserve discounted bread.
  5. Switch the interface language.
- **Metrics:** task success rate, completion time, number of errors.

### Post-Test Questionnaire

Based on the IS Success Model and TAM (Song et al., 2023); 5-point Likert scale.

1. The application is easy to use.
2. The calculation of my share is clear.
3. I trust the payment method.
4. The application will help me save money on food.
5. I would continue using the application.
6. I would recommend it to my neighbours.

**Success criterion:** mean score ≥ 4.0 for items 1, 4 and 5; System Usability Scale (SUS) score ≥ 68.

## 9.4 Savings Evaluation

| Product | Retail price, KZT | Pool price, KZT | Savings, % |
|---------|-------------------|-----------------|------------|
| Flour, first grade, 1 kg | | | |
| Potatoes, 1 kg | | | |
| Sunflower oil, 1 L | | | |
| Sugar, 1 kg | | | |
| **Basket** | | | |

Retail prices are taken from BNS socially significant food product monitoring; wholesale prices from supplier interviews and wholesale market price lists.

## 9.5 Schedule

| Activity | Timing |
|----------|--------|
| Unit tests of allocation algorithm | After backend implementation |
| Usability test | After UX prototype completion |
| Questionnaire analysis | Immediately after usability test |
| Savings evaluation | Before pre-defence |
