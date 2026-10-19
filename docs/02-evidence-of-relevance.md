# 2. Evidence of Relevance

## 2.1 Problem Statement

Low-income and large families in Kazakhstan spend more than half of their consumer budget on food. Wholesalers and farmers offer lower prices, but their minimum order quantities (a 50 kg bag of flour, a case of oil, a sack of potatoes) are too large for a single household to pay for at once or to store. At the same time, retailers and bakeries write off edible products close to their expiry date that the same families could buy at a discount.

The project addresses three related problems:

1. **High share of food in household spending.**
2. **Wholesale quantity barrier:** wholesale prices are lower, but the batch size is too large for one family.
3. **Waste of edible food** in retail due to the lack of a convenient redistribution channel.

## 2.2 Secondary Data

| # | Indicator | Value | Source |
|---|-----------|-------|--------|
| 1 | Share of food in household consumer spending, Q3 2025 | **57.2%** (rural 58.7%, urban 56.5%); 10–15% in developed countries | Kapital.kz, based on BNS ASPR RK |
| 2 | Food spending, Q4 2025 (sample of 11,712 households) | KZT 579,685 per quarter, **57%** of consumption; spending equalled 90.4% of income | BNS ASPR RK via BAQ.kz / DairyNews |
| 3 | Largest food spending categories | meat 16.9%, bread and cereals 7.7% | stat.gov.kz |
| 4 | Annual price growth of socially significant food products (SSFP, 31 items) | Jan 2026: **+7.1%**; Apr 2026: +5.1%; Jul 2026: +2.9%; Aug 2026: +2.1% | Finratings.kz; Kazinform; Zakon.kz |
| 5 | Annual meat price growth, April 2026 | lamb +22.0%, boneless beef +20.9%, minced meat +19.5% | Kazinform, based on BNS |
| 6 | Regional SSFP price growth, April 2026 | Aktau +9.1%, Zhezkazgan +8.0%, Taldykorgan +7.2% | DairyNews.today |
| 7 | Temporarily extended SSFP list | in force since 4 January 2026 | Kapital.kz |
| 8 | Recipients of targeted social assistance (TSA), 1 April 2026 | 167,400 people in 31,100 families | Ministry of Labour via Kapital.kz |
| 9 | Large families receiving state benefits | over 630,000 families | 24.kz |
| 10 | Food waste in Kazakhstan (UNEP Food Waste Index 2024) | **82.99 kg per capita per year**, about **1.7 million tonnes per year** | Baidalinova et al., 2025 |
| 11 | Barrier to food donation | businesses pay the same taxes on donated food, so disposal is cheaper | Informburo.kz |

**Interpretation.** Although SSFP inflation slowed in mid-2026, food still accounts for about 57% of household spending, and meat prices rose by more than 20% in a year, which shows that the problem is structural rather than temporary. At the same time, about 1.7 million tonnes of food are wasted annually. The proposed system connects both sides: collective wholesale purchasing lowers prices for families, and the food-sharing module gives retailers an alternative to write-offs.

## 2.3 Primary Data: Interviews

### 2.3.1 Method

- **Format:** structured written interviews conducted via a messaging app (WhatsApp), October 2026.
- **Participants:** 3 respondents from households in Kazakhstan, recruited through the author's personal network.
- **Ethics:** participants were informed of the purpose of the study and agreed to take part anonymously. No names, IIN or addresses were recorded. The original messages are kept by the author.

| ID | Household size | Usual place of purchase |
|----|----------------|-------------------------|
| R1 | 3 people | Supermarkets and local shops; bazaar when cheaper |
| R2 | 3 people | Small (supermarket chain) |
| R3 | 6 people | Supermarkets and a food bazaar |

### 2.3.2 Questions

1. How many people are in your household, and where do you usually buy food?
2. Approximately what share of your budget is spent on food? What has become most expensive?
3. Have you ever bought food in bulk (a bag of flour, a case of oil) or together with neighbours? What prevented you?
4. Would you use an app that lets neighbours buy together from a farmer 20–30% cheaper? What would stop you?
5. Would you buy bread or dairy products close to their expiry date at a 50–70% discount?
6. How do you prefer to pay (Kaspi QR, cash), and where would you like to collect your order?

### 2.3.3 Results

| Topic | R1 | R2 | R3 |
|-------|----|----|----|
| Food spending | 30–40% of budget | 20–30% (estimate; the mother does the shopping) | KZT 150,000–200,000 per month |
| Largest price increases | Meat and vegetables | Not known | Affordable high-quality dairy is hard to find |
| Bulk purchasing experience | Yes, at fairs; pooled 6–7 bags of sugar with neighbours and relatives in 2022–2023 | No | Yes, often; even fruit by the crate |
| Barriers to bulk purchasing | Large upfront payment; lack of storage space | — | — |
| Willingness to use the app | Yes, if the farmer is reliable and delivery is on time | Yes, would try it | Yes, gladly |
| Near-expiry food at a discount | Yes, if it does not expire the same day and was stored properly | No, freshness matters more than price | No |
| Payment method | Kaspi QR | Kaspi QR | Kaspi QR |
| Collection preference | Home delivery | — | Delivery preferred; self-collection if a car is available |

### 2.3.4 Key Quotations

- **R1:** “In 2022–2023 we already chipped in with neighbours and relatives for 6–7 bags of sugar, so we have the experience. The main thing is that the farmer is reliable and the order arrives on time.”
- **R1:** “What usually stops us is having to spend a large amount at once and having no space to store it.”
- **R2:** “For me, freshness is more important than price.”
- **R3:** “I would gladly use it, because it is hard to find quality dairy products at an affordable price.”

### 2.3.5 Summary of Findings

1. **Demand for the core idea is confirmed.** All three respondents would use the collective purchasing app; two already buy in bulk, and one has organised a joint purchase with neighbours.
2. **The main barriers are upfront cost and storage**, which the pool model addresses directly by splitting both cost and quantity.
3. **Trust in the supplier and delivery reliability** are the key conditions for participation.
4. **Kaspi QR is the unanimous payment preference.**
5. **Home delivery is preferred** by two of three respondents over self-collection.
6. **Acceptance of near-expiry food is low** (one of three, conditionally). Respondents associate it with poor freshness, so the food-sharing module must be positioned carefully.
7. Reported food spending (20–40%) is lower than the national average of 57%. This is expected because the sample consists of urban households that do not belong to the low-income target group.

### 2.3.6 Limitations

The sample is small (n = 3) and consists of urban households from the author's personal network rather than low-income or large families. Suppliers, retailers and building representatives were not interviewed. The findings are therefore treated as exploratory and are complemented by the national statistics in Section 2.2.

## 2.4 Implications for Requirements

| Finding | System requirement |
|---------|--------------------|
| Food is about 57% of spending nationally; meat prices rise fastest | Catalogue prioritising SSFP; display savings against retail prices |
| Upfront cost and lack of storage prevent bulk buying (R1) | Purchase pools with automatic calculation of each family's share |
| Previous joint purchases were organised manually (R1) | Pool creation, joining and closure handled by the system |
| Supplier reliability and on-time delivery are key conditions (R1) | Supplier ratings and reviews; delivery date shown on each pool |
| Kaspi QR preferred by all respondents | Individual payment by Kaspi QR for each family |
| Home delivery preferred (R1, R3) | Pick-up point as default; optional supplier delivery to the address |
| Freshness concerns about near-expiry food (R1, R2, R3) | Exact expiry date, storage conditions and photo shown for every food-sharing listing; listings removed before the expiry date |
| Demand for affordable quality dairy (R3) | Dairy category from local farmers in the catalogue |
| TSA is granted below the poverty line | Optional “social family” status with an additional discount, verified by an administrator |

## References

- Bureau of National Statistics ASPR RK. Food consumption of households. https://stat.gov.kz/ru/industries/labour-and-income/stat-life/publications/365313/
- Kapital.kz. Share of Kazakhstanis' spending on food reached 57%. https://kapital.kz/economic/145041/dolya-rashodov-kazahstancev-na-prodovolstvie-dostigla-57percent.html
- DairyNews.today. Kazakhstan households spend more than half of their budget on food. https://dairynews.today/kz/news/kazakhstanskie-domokhozyaystva-tratyat-na-edu-bolshe-poloviny-byudzheta-statistika.html
- Finratings.kz. Meat is already a luxury. https://finratings.kz/news/11499-miaso-uzhe-roskosh-kak-bazovye-produkty-vytalkivaiut-kazakhstantsev-za-predely-biudzheta/
- Kazinform. How food prices changed in Kazakhstan (April 2026). https://www.inform.kz/ru/kak-izmenilis-tseni-na-produkti-v-kazahstane-987d2a
- Kazinform. How prices changed over the year (July 2026). https://www.inform.kz/ru/kak-izmenilis-tseni-dlya-kazahstantsev-za-god-na-sotsialno-znachimie-produkti-6d3d922a
- Zakon.kz. Price growth in Kazakhstan slowed sharply (August 2026). https://www.zakon.kz/finansy/6529727-tseny-v-kazakhstane-rezko-zamedlili-rost-chto-podorozhalo-i-chto-podeshevelo.html
- DairyNews.today. SSFP price growth widened the regional gap. https://dairynews.today/kz/news/rost-tsen-na-sotsialno-znachimye-produkty-usilil-regionalnyy-razryv-v-kazakhstane.html
- Kapital.kz. Extended SSFP list. https://kapital.kz/economic/144182/otpusknye-ceny-na-yajca-myaso-kur-maslo-kartofel-hotyat-zafiksirovat-na-god.html
- Kapital.kz. 167,000 Kazakhstanis received TSA by 1 April. https://kapital.kz/economic/146670/k-1-aprelya-adresnuyu-socialnuyu-pomosh-poluchili-167-tysyach-kazahstancev.html
- 24.kz. 630,000 large families receive benefits. https://24.kz/ru/news/social/775052-630-tysyach-mnogodetnykh-semej-poluchayut-posobiya
- Baidalinova, A.S., Baigireeva, Zh.Z., & Niyazbekova, Sh.U. (2025). Economic aspects of food waste management in Kazakhstan. *Bulletin of L.N. Gumilyov ENU, Economics Series*, (2), 143–162. https://doi.org/10.32523/2789-4320-2025-2-143-162
- Informburo.kz. Why it is more profitable for supermarkets to throw food away. https://informburo.kz/novosti/pocemu-supermarketam-v-kazaxstane-vygodnee-vybrasyvat-produkty-cem-razdavat-nuzdayushhimsya