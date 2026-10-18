# 3. Literature Review

## 3.1 Search Method

- **Databases:** Google Scholar, ScienceDirect, MDPI, Frontiers, Emerald, SHS Web of Conferences, CyberLeninka, Kazakhstani university journals.
- **Keywords:** community group buying, online group buying trust, food sharing app, surplus food redistribution, food sales prediction machine learning, food waste Kazakhstan.
- **Inclusion criteria:** published 2011–2025; topic covers group purchasing, food sharing, food demand forecasting or the Kazakhstani context; abstract or full text available.
- **Exclusion criteria:** promotional content, sources without author or date.

The review includes 16 sources: 12 scientific (peer-reviewed journals, conference proceedings, academic book chapters) and 4 statistical or legal sources.

## 3.2 Thematic Review

### Theme A. Collective (Group) Purchasing

**[1] Liu et al. (2013)** examined why Chinese consumers join online group buying. Price, convenience and recreational benefits, together with trust in the initiator (reputation, structural assurance, website trustworthiness), positively influence attitudes. *Relevance:* low price alone is insufficient; the system should show organiser ratings and guarantee refunds.

**[2] Wu, Chen, Pan and Xu (2022)** surveyed 430 community group-buying consumers in Fuzhou. The group leader influences loyalty through two roles: “merchant” (information, fast responses, after-sales service) and “friend” (help, social interaction). Trust in the leader transfers to trust in the platform, and platform trust has the strongest effect on repeat purchasing. *Relevance:* a building representative as pool organiser is justified, but the platform itself must provide guarantees such as transparent share calculation and order history.

**[3] Si (2024)** describes how community group leaders collect orders, liaise with suppliers and distribute goods; regular interaction increases their influence and neighbours' trust. *Relevance:* supports the “organiser + pick-up point” model.

**[4] SHS Web of Conferences (2023)** decomposes the community group-purchasing supply chain into shared warehouse, central warehouse, front distribution centre, group leader and consumer, showing reduced last-mile costs. *Relevance:* one combined order per district pick-up point is the core source of savings.

**[5] Song, Gui, Yang et al. (2023)** combined the DeLone and McLean IS Success Model and an extended Technology Acceptance Model to show that system, information and service quality, perceived usefulness and ease of use drive continued use of group-buying platforms. *Relevance:* provides a validated framework for the evaluation questionnaire (Section 9).

### Theme B. Food Sharing and Surplus Redistribution

**[6] Michelini, Principato and Iasevoli (2018)** analysed 52 food-sharing platforms and identified three models: for-profit B2C (discounted surplus), non-profit B2C, and peer-to-peer. *Relevance:* the proposed module follows the for-profit B2C model with a social objective.

**[7] Harvey, Smith, Goulding and Branco Illodo (2020)** performed a social network analysis of 54,913 food-sharing instances among 9,054 OLIO users over ten months. Reciprocity was rare: most users acted only as donors or only as recipients. *Relevance:* the module should rely on business suppliers (shops, bakeries) rather than peer exchange.

**[8] Makov, Shepon, Krones, Gupta and Chertow (2020)** analysed about 170,000 OLIO listings; around 90 tonnes of food were redistributed in 19 months. They note that private car trips to collect food can offset environmental gains. *Relevance:* food-sharing collection should use the same pick-up points as pools.

**[9] Baidalinova, Baigireeva and Niyazbekova (2025)** analysed food waste in Kazakhstan, citing UNEP estimates of about 83 kg per capita and 1.7 million tonnes per year, and proposed digital platforms for redistributing surplus food. *Relevance:* direct academic justification for the food-sharing module in Kazakhstan.

**[10] Kaliyeva et al. (2024)** used contingent valuation to show that Kazakhstani households are willing to support waste-reduction policy, with age and eco-friendly lifestyle as significant factors. *Relevance:* indicates public readiness to participate in sustainability initiatives.

### Theme C. Demand Forecasting

**[11] Tsoumakas (2019)** reviewed machine learning approaches to food sales prediction, including temporal granularity, input variables and accuracy metrics; accurate short-term forecasts reduce both expired stock and missed sales. *Relevance:* basis for district-level SSFP demand forecasting (features: weekday, season, price, holidays).

**[12] Aichner and Santa (2023)** compared traditional and ML forecasting in grocery retail through expert interviews and identified staff, data and ERP readiness as prerequisites. *Relevance:* the system should start with a simple baseline model and move to ML once enough order data is collected.

### Theme D. Statistical and Legal Context

**[13] Bureau of National Statistics:** household spending on food.
**[14] UNEP Food Waste Index Report 2024:** country-level food waste estimates.
**[15] SSFP price monitoring (BNS, Kazinform):** weekly prices of 31 socially significant food products.
**[16] Social Code of the Republic of Kazakhstan, Article 120:** TSA is granted when per-capita income does not exceed the poverty line; basis for the social status module.

## 3.3 Analysis Table

| # | Source | Type | Method | Key finding | Use in project | Limitation |
|---|--------|------|--------|-------------|----------------|------------|
| 1 | Liu et al., 2013 | Journal | Survey, SEM | Price, convenience and trust shape attitudes | Organiser rating, guarantees | China, pre-mobile era |
| 2 | Wu et al., 2022 | Journal | Survey (n=430), SEM | Trust in leader transfers to platform | Organiser role + platform guarantees | Single city |
| 3 | Si, 2024 | Conference | Theoretical analysis | Leader stabilises the group | Building representative model | No empirical data |
| 4 | SHS Web Conf., 2023 | Conference | Supply chain analysis | Group delivery lowers last-mile cost | Combined order per pick-up point | Descriptive |
| 5 | Song et al., 2023 | Journal | D&M + TAM survey | Quality and usefulness drive continued use | Evaluation questionnaire | China |
| 6 | Michelini et al., 2018 | Journal | Review of 52 platforms | Three food-sharing models | Choice of B2C model | Europe |
| 7 | Harvey et al., 2020 | Journal | Social network analysis | Reciprocity is rare | Rely on business suppliers | OLIO, UK only |
| 8 | Makov et al., 2020 | Journal | NLP, GIS, LCA | P2P sharing works; transport offsets gains | Shared pick-up points | P2P, not B2C |
| 9 | Baidalinova et al., 2025 | Journal | Statistical analysis | ~1.7 Mt food waste per year in Kazakhstan | Local justification | Limited retail data |
| 10 | Kaliyeva et al., 2024 | Journal | Contingent valuation | Public supports waste policy | User readiness | Municipal waste, not food |
| 11 | Tsoumakas, 2019 | Journal | Literature survey | ML methods for food sales | Feature and metric choice | No Kazakhstani data |
| 12 | Aichner & Santa, 2023 | Book chapter | Expert interviews | ML needs data, staff, ERP | Phased AI adoption | Large retailers |
| 13 | BNS RK | Statistics | Household survey | Food ≈ 57% of spending | Problem evidence | — |
| 14 | UNEP, 2024 | UN report | Waste index | Country estimates | Kazakhstan figures | Modelled estimates |
| 15 | BNS / Kazinform, 2026 | Monitoring | Weekly prices | SSFP and meat inflation | SSFP-first catalogue | Changes weekly |
| 16 | Social Code RK | Law | — | TSA eligibility by poverty line | Social status module | — |

## 3.4 Research Gap

1. Almost all group-buying studies focus on China, with large platforms and dense logistics. No studies of collective grocery purchasing in Kazakhstan were found.
2. Group purchasing and food sharing are studied separately; no system combining both for low-income families was identified.
3. None of the reviewed solutions accounts for a family's social status (TSA, large family) in pricing.

The proposed system addresses this gap by combining district purchase pools, B2C food sharing and social-status-aware pricing, adapted to Kazakhstan (Kaspi QR, condominium associations, Kazakh and Russian languages).

## 3.5 References

1. Liu, M. T., Brock, J. L., Shi, G. C., & Chu, R. (2013). Perceived benefits, perceived risk, and trust: Influences on consumers' group buying behaviour. *Asia Pacific Journal of Marketing and Logistics, 25*(2). https://doi.org/10.1108/13555851311314031
2. Wu, J., Chen, Y., Pan, H., & Xu, A. (2022). Influence of multi-role interactions in community group-buying on consumers' lock-in purchasing intention from a fixed leader based on role theory and trust transfer theory. *Frontiers in Psychology, 13*, 903221. https://doi.org/10.3389/fpsyg.2022.903221
3. Si, X. (2024). How group leaders build stable community buying groups: A perspective based on the differential mode of association. *SHS Web of Conferences, 181*, 01032. https://doi.org/10.1051/shsconf/202418101032
4. Analysis of community group purchasing in China during the COVID-19 period. (2023). *SHS Web of Conferences, 154*, 01006. https://doi.org/10.1051/shsconf/202315401006
5. Song, Y., Gui, L., Yang, Y., et al. (2023). Determinants of continuous usage intention in community group buying platform in China: Based on the information system success model and the expanded technology acceptance model. *Behavioral Sciences, 13*(11), 941. https://doi.org/10.3390/bs13110941
6. Michelini, L., Principato, L., & Iasevoli, G. (2018). Understanding food sharing models to tackle sustainability challenges. *Ecological Economics, 145*, 205–217. https://doi.org/10.1016/j.ecolecon.2017.09.009
7. Harvey, J., Smith, A., Goulding, J., & Branco Illodo, I. (2020). Food sharing, redistribution, and waste reduction via mobile applications: A social network analysis. *Industrial Marketing Management, 88*, 437–448. https://doi.org/10.1016/j.indmarman.2019.02.019
8. Makov, T., Shepon, A., Krones, J., Gupta, C., & Chertow, M. (2020). Social and environmental analysis of food waste abatement via the peer-to-peer sharing economy. *Nature Communications, 11*, 1156. https://doi.org/10.1038/s41467-020-14899-5
9. Baidalinova, A. S., Baigireeva, Zh. Z., & Niyazbekova, Sh. U. (2025). Economic aspects of food waste management in Kazakhstan: Problems, trends, and prospects. *Bulletin of L.N. Gumilyov Eurasian National University, Economics Series*, (2), 143–162. https://doi.org/10.32523/2789-4320-2025-2-143-162
10. Kaliyeva, S. S., et al. (2024). Economic assessment of MSW reduction policy in the Republic of Kazakhstan using the contingent valuation method. *Bulletin of Turan University*, (3), 23–34. https://doi.org/10.46914/1562-2959-2024-1-3-23-34
11. Tsoumakas, G. (2019). A survey of machine learning techniques for food sales prediction. *Artificial Intelligence Review, 52*, 441–447. https://doi.org/10.1007/s10462-018-9637-z
12. Aichner, T., & Santa, V. (2023). Demand forecasting methods and the potential of machine learning in the FMCG retail industry. In T. Aichner (Ed.), *Serving the Customer* (pp. 215–252). Springer.
13. Bureau of National Statistics ASPR RK. (2025). Food consumption of households. https://stat.gov.kz/ru/industries/labour-and-income/stat-life/publications/365313/
14. United Nations Environment Programme. (2024). *Food Waste Index Report 2024*. https://wedocs.unep.org/20.500.11822/45230
15. Kazinform. (2026). How food prices changed in Kazakhstan. https://www.inform.kz/ru/kak-izmenilis-tseni-na-produkti-v-kazahstane-987d2a
16. Social Code of the Republic of Kazakhstan of 20 April 2023, Article 120. https://prg.kz/m/amp/document/36102527/12/1360000
