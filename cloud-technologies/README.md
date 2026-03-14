# 🎓 Analysis of Opportunities for International Students in Japan

**Course:** Cloud Technologies and Big Data Frameworks  
**Institution:** Politecnico di Milano – Graduate School of Management  
**Group 5:** Maxime Engels, Lucia Francescoli, Tiziano Gallo, Frank Novoa

---

## 📌 Overview

This project analyzes the best universities and regions in Japan for international students, taking into account internationalization, research impact, graduate employability, and regional living expenditure. The goal is to identify top opportunities and detect geographic inequalities that could hinder the attraction of global talent.

---

## ❓ Research Question

> *Which universities and regions in Japan offer the best opportunities for international students, considering internationalization, research impact, employability, and regional living expenditure — and where do geographic gaps or inequalities exist?*

---

## 🗂️ Datasets

| Dataset | Description |
|---|---|
| **Japan Top Universities** | 52 leading universities with research impact score, international student ratio, employment rate, institution type, and region code |
| **Japan Region** | Population data for all 47 Japanese prefectures (2024) |
| **Japan Expenditure** | Average monthly living expenditure by prefecture (in Yen, 2007) |

**Source:** [Kaggle – Japan Top 50 Universities Dataset](https://www.kaggle.com/datasets/nudratabbas/japan-top-50-universities-dataset) | [e-Stat Japan](https://www.e-stat.go.jp/en/regional-statistics/ssdsview/prefectures)

---

## 🛠️ Tech Stack

- **Apache Spark (PySpark)** – distributed data processing
- **Google Colab** – cloud notebook environment
- **Python** – pandas, seaborn, matplotlib for analysis and visualization
- **Google Drive** – dataset storage and access

---

## 📊 Key Findings

- **Highest international student ratio:** Ritsumeikan Asia Pacific University (48.5%), followed by Akita International University and International Christian University.
- **Most universities per region:** Tokyo leads with 14 top universities, followed by Kyoto and Osaka with 3 each.
- **Institution type & internationalization:** Public universities have the highest average international student ratio (15.3%), ahead of Private (12.4%) and National (8.6%).
- **Top employability:** Private and National universities dominate — Shibaura Institute of Technology ranks #1 at 98.2%. Public universities do not appear in the top 10.
- **Overall best opportunity score:** University of Tokyo (69.1), followed by Institute of Science Tokyo and Kyoto University.
- **Most cost-efficient top university:** Osaka University — strong rankings at lower living costs than Tokyo.
- **Geographic inequality:** Saitama has the lowest university density relative to its population.

---

## ✅ Conclusions

1. **Tokyo** offers the highest concentration of top universities and employment opportunities, but also the highest living costs.
2. **Kyoto and Osaka** provide comparable academic quality and employability to Tokyo at lower living expenditure — making them highly attractive alternatives.
3. **Public universities** across Japan are the most internationally welcoming, with the highest share of international students.
4. The best opportunities come from **balancing** internationalization, employability, research quality, and affordability — not from chasing rankings or major cities alone.

---

## 📁 Repository Structure

```
polimi-gsom-projects/
│
└── cloud-technologies/
    ├── FinalWorkCloud.ipynb       # Main analysis notebook (PySpark + visualizations)
    ├── japan_universities_2026.csv
    ├── region_japan_2024.csv
    └── japan_expenditure.csv
```

---

## 🚀 How to Run

1. Upload the datasets to your Google Drive under `Colab Notebooks/BADS2026/FinalWorkCloud/`
2. Open `FinalWorkCloud.ipynb` in Google Colab
3. Mount your Drive and run all cells in order
