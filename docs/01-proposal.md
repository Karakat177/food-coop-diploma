# 1. Project Proposal

## 1.1 Title

**Information System for Optimizing Collective Food Purchasing and Redistribution**

## 1.2 Problem

In Kazakhstan, food accounts for about 57% of household consumer spending (Bureau of National Statistics, Q3–Q4 2025), compared with 10–15% in developed countries. Prices of socially significant food products continue to rise; meat prices increased by 19–22% in the year to April 2026. Wholesalers and farmers sell at lower prices, but their minimum order quantities are too large for a single low-income or large family. At the same time, Kazakhstan generates about 1.7 million tonnes of food waste per year (UNEP, 2024), and retailers find it cheaper to dispose of food than to donate it. No digital tool in Kazakhstan currently enables neighbours to buy in bulk together or gives them access to discounted surplus food (see Section 4).

## 1.3 Target Users

| Group | Description | Need |
|-------|-------------|------|
| Families (primary) | Large families, low-income households, TSA recipients and other residents | Buy staple food below retail price |
| Pool organiser | Building representative, head of condominium association, active resident | Collect orders and payments easily, distribute goods |
| Suppliers | Farmers, wholesalers, small distributors | Sell large batches in a single order |
| Retailers and bakeries | Local shops | Sell products close to expiry instead of writing them off |
| Administrator | Platform team | Moderate suppliers, verify social status |

## 1.4 Goal

To develop a mobile and web application that allows families in the same district to form purchase pools and buy food at wholesale prices directly from suppliers, automatically calculates each family's share and QR payment, and provides access to discounted products close to their expiry date.

**Objectives:**

1. Reduce the cost of a basket of socially significant food products for pool participants by at least **15%** compared with the average retail price in the district.
2. Enable a new user to create or join a pool in **no more than 3 minutes**.
3. Achieve **100% correctness** of share and total calculations across all test scenarios.
4. Provide a fully bilingual interface in **Kazakh and Russian**.

## 1.5 Scope

**In scope (MVP):**

- Family registration and district/building selection
- Supplier catalogue with wholesale prices and minimum order quantities
- Pool creation and joining, automatic share calculation, automatic pool closure when the target is reached
- QR code generation for individual payment (Kaspi integration in sandbox mode)
- Combined order sent to the supplier
- Map of pick-up points
- Food-sharing module: retailers list discounted near-expiry products, families reserve them
- Supplier web portal
- “Social family” status with manual document verification by an administrator
- Baseline demand forecast for socially significant food products by district

**Out of scope:**

- In-house delivery service and warehousing
- Live integration with government databases (TSA, eGov)
- Real payment processing (test environment only)
- Sale of alcohol, tobacco and medicines
- Multi-city launch (pilot in one district of Astana)

## 1.6 Expected Outcome

A working prototype (mobile application, web portal and backend), tested on pool and food-sharing scenarios, with savings and usability evaluated according to the verification plan (Section 9).
