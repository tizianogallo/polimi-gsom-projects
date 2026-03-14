# 🌐 Levelling the Field: A Statistical Analysis on Internet Connection across Europe

**Course:** Fundamentals of Statistics | BADS  
**Institution:** Politecnico di Milano – Graduate School of Management  
**Team:** Luca Stucchi, Stole Donev, Maxime Engels, Tiziano Gallo

---

## 📌 Overview

This project statistically analyzes broadband internet connectivity across European regions (NUTS 2 level), with the goal of informing the **European Commission** on where to prioritize investment under the **EU Digital Decade 2030** target — 100% gigabit internet for all EU households by 2030.

In 2020, only 13% of regions met even 100 Mbps. By 2022, that number rose to 62%, but 38% of regions still lag behind — and internal inequalities within countries are growing.

---

## ❓ Research Questions

| # | Question |
|---|---|
| **RQ1** | Are EU regions converging towards the 100 Mbps target? What structural factors drive the remaining gap? |
| **RQ2** | Is internet access really equal across EU regions, or does download speed hide a deeper divide? |
| **RQ3** | Which regions are most suitable for satellite internet? Where should the EU prioritize last-mile investment? |

---

## 🗂️ Data

**Source:** [Eurostat](https://ec.europa.eu/eurostat) — Broadband Infrastructure Data

| Dataset | Key Variables |
|---|---|
| **Speed** | `nuts_code`, `year`, `download_speed`, `upload_speed`, `latency` |
| **Household Access** | `nuts_code`, `year`, `household_access_pct` |
| **Price** | `nuts_code`, `year`, `service_tier`, `price_eur` |
| **GDP** | `nuts_code`, `year`, `gdp_million_eur` |
| **Density** | `nuts_code`, `year`, `people_per_sqkm` |
| **Population** | `nuts_code`, `year`, `total_population` |
| **Income** | `nuts_code`, `year`, `income_million_eur` |

All datasets are linked via `nuts_code` (NUTS 2 regional identifier).

---

## 🛠️ Tech Stack

- **R** — primary language for all statistical analysis and visualization
- **ggplot2** — data visualization (bar charts, box plots, scatter plots, Lorenz curves)
- **PCA (Principal Component Analysis)** — dimensionality reduction for satellite suitability scoring
- **Gini / Lorenz Curve Analysis** — measuring within-country inequality

---

## 📊 Key Findings

- **Progress is real but uneven:** median download speed grew from 65 Mbps (2020) to 113 Mbps (2022), but 140 regions still fall below 100 Mbps.
- **Red Zone countries** (median household access <90%): Serbia, Croatia, Bulgaria, Romania, Lithuania, Portugal.
- **Most underserved regions** (low speed + high price): predominantly Greek regions (Ionia Nisia, Sterea Elláda, Peloponnisos, etc.) and Prov. Luxembourg (BE).
- **Internal inequality is the hidden problem:** Gini analysis shows Serbia, France, and Czechia have the highest within-country download speed inequality, even when national averages look acceptable.
- **Satellite-optimal regions** (low PC1 infrastructure, positive PC2 price tolerance): N. Macedonia, Jadranska Hrvatska, Panonska Hrvatska, Calabria, and several Austrian regions lead the target list.

---

## 🔬 Statistical Methods

- **Descriptive statistics** — median speed, household access rates, regional counts
- **Box plots & histograms** — distribution of household access by country (2020 vs 2022)
- **Lorenz curves & Gini coefficients** — inequality of household access and download speed within countries
- **PCA (2 components retained via Kaiser Criterion, λ>1):**
  - PC1 (50.7%) — "rich & connected" composite (all 5 variables load positively)
  - PC2 (22.8%) — speed & density vs income & GDP (separates dense/fast/poor from sparse/wealthy)
- **Satellite Suitability Index** — derived from PCA scores to rank the top 15 regions for satellite internet deployment

---

## ✅ Conclusions

1. **Equal access, but not enough speed** — household connectivity is broadly improving, but actual speeds remain insufficient in many regions.
2. **South-East Europe is being left behind** — the Balkans and southeastern periphery consistently underperform on both speed and access.
3. **Internal inequality is the hidden problem** — national averages mask severe regional disparities within countries like Serbia, France, and Czechia.
4. **Some countries are paying more for less** — Greece and Belgium show high broadband prices relative to the speeds delivered.

---

## 💡 Recommendations

1. **Target Red-Zone countries** — direct EU Cohesion Funds to Serbia, Croatia, Bulgaria, Romania, Lithuania, and Portugal
2. **Address speed inequality, not just access** — household connectivity rates are converging, but speed gaps are widening
3. **Pilot satellite internet in the top 15 identified regions** — especially N. Macedonia, Croatia, and Calabria
4. **Improve infrastructure & reduce the price gap** — particularly in Greece and Belgium
5. **Expand data collection to NUTS 3 level** — NUTS 2 aggregation masks sub-regional gaps

---

## ⚠️ Limitations

- **Cross-sectional snapshot** — 2022 data only; no long-term causal trend analysis
- **Missing price data** — 10 countries excluded (Serbia, Norway, Switzerland, UK, etc.)
- **No satellite penetration data** — all measurements are terrestrial
- **NUTS 2 aggregation** — unable to pinpoint exact sub-regional problem areas

---
