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

### 2.3.1 Participants

| ID | Profile | Purpose |
|----|---------|---------|
| R1 | Parent in a large family (3+ children) | Primary user; cost of food |
| R2 | Low-income household or TSA recipient | Budget constraints |
| R3 | Building representative / head of condominium association (OSI/KSK) | Pool organiser and pick-up point |
| R4 | Farmer, wholesale market seller or small distributor | Supplier: minimum order, volume discount |
| R5 | Grocery store or bakery manager | Food sharing: write-offs and their causes |

### 2.3.2 Protocol

- Duration: 15–25 minutes, in person or online.
- Verbal informed consent was obtained before each interview. No names, IIN or addresses were recorded.
- Responses were recorded in note form close to the participant's words and summarised immediately after the session.

### 2.3.3 Interview Guide: Families (R1, R2)

1. How many people are in your household? Who usually buys groceries?
2. Where do you usually buy food (local shop, supermarket, bazaar, wholesale market, online)? Why there?
3. Approximately what share of your family budget goes on food? Has it changed over the past year?
4. Which products have become noticeably more expensive for you?
5. Have you ever bought food in bulk (a bag of flour, a case of oil)? If not, what prevented you (upfront cost, storage, transport)?
6. Have you ever bought together with neighbours or relatives? How did you split the cost and the goods? Were there any problems?
7. How much do you trust neighbours in joint purchases? What would increase that trust?
8. Would you use an app that brings neighbours together to buy from a farmer 20–30% cheaper than in a shop? What would stop you?
9. How do you prefer to pay: Kaspi QR, bank transfer, cash?
10. Would you buy products close to their expiry date (bread, dairy) at a 50–70% discount? Which products yes, which no?
11. Where would it be convenient to collect an order: building entrance, building representative, condominium office, shop?
12. Which language do you prefer for the app: Kazakh or Russian?

### 2.3.4 Interview Guide: Other Stakeholders

**Building representative (R3):** Is there a residents' chat and how active is it? Have joint purchases been organised before? Would you act as a pick-up point? What would you expect in return? What conflicts do you anticipate?

**Supplier (R4):** What is your minimum order quantity? What is the difference between wholesale and retail prices? Do you sell to groups of buyers? How do you accept payment? What prevents you from selling directly to families? Would you deliver one combined order to a single point in a district?

**Retailer (R5):** How much product is written off per day or week? What happens to it now? Why is it not donated or sold at a discount? Would you list such products in an app two to three hours before closing?

### 2.3.5 Results

| Topic | R1 | R2 | R3 | R4 | R5 | Finding |
|-------|----|----|----|----|----|---------|
| Main pain point | | | | | | |
| Experience of joint purchasing | | | | | | |
| Willingness to use the app (1–5) | | | | | | |
| Preferred payment method | | | | | | |
| Preferred pick-up point | | | | | | |
| Preferred language | | | | | | |

**Key quotations:**

- R1: “…”
- R2: “…”
- R3: “…”
- R4: “…”
- R5: “…”

## 2.4 Implications for Requirements

| Finding | System requirement |
|---------|--------------------|
| Food is about 57% of spending; meat prices rise fastest | Catalogue prioritising SSFP; display savings against retail prices |
| Wholesale batches are too large for one family | Purchase pools with automatic calculation of each family's share; pool closes when the target quantity is reached |
| Low trust when one person collects money | Individual QR payment per family; funds released to the supplier only when the pool is complete; organiser rating |
| Retail write-offs of edible food | Food-sharing module with time-limited discounted listings |
| Users speak Kazakh and Russian | Bilingual interface (KZ/RU) |
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
