# Yeti Travel Agency — Customer Churn Prediction
 
**Machine Learning & Business Applications — Politecnico di Milano**  
Stole Donev, Maxime Engels, Tiziano Gallo, Luca Stucchi
 
---
 
## 🎯 Overview
 
Yeti Travel Agency specializes exclusively in school trip packages. The agency detected a noticeable drop in sales among regular customers and tasked us with building a predictive model to identify which schools are at risk of churning.
 
**Goal:** Predict whether a school will return the following year (`Retained = 1`) or not (`Retained = 0`) using historical data from three internal departments — Sales, Finance, and CRM.
 
This is a **binary classification** problem with three stages:
1. Build a predictive model to estimate churn probability
2. Identify the most informative features driving retention
3. Translate findings into actionable business recommendations
---
 
## 📦 Dataset
 
Three pairs of CSV files — one pair per department:
 
| Dataset | Training rows | Test rows | Fields |
|---|---|---|---|
| Sales (`sales_model.csv` / `sales_test.csv`) | 4,153 | 630 | 24 |
| Finance (`finance_model.csv` / `finance_test.csv`) | 4,151 | 630 | 12 |
| CRM (`crm_model.csv` / `crm_test.csv`) | 4,148 | 630 | 20 |
 
Training files contain the `Retained` target column. Test files do not — these are the records to predict.
 
---
 
## ⚙️ Pipeline
 
### 1. ID Normalisation
Each department uses its own ID format:
- Sales: `CC1387A`
- Finance: `NA1387`
- CRM: `B1387K`
A shared numeric key (`1387`) was extracted from each ID and used to perform a 3-way inner join.
 
### 2. Data Merging
- **Training set:** 3-way inner join on numeric ID → **3,095 rows** retained (74.5% of original)
- **Test set:** positional concat to preserve all 630 records
### 3. Preprocessing Pipeline (leakage-free)
All steps fitted only on training data, then applied to validation and test:
- European decimal conversion (`0,123` → `0.123`)
- Date feature engineering:
  - `Days_System_to_Departure` — planning lead time
  - `RPL_Window_Days` — recruitment window length
  - `Departure_Month_Num` — month of departure
- Median imputation for numeric, constant `"Missing"` for categorical
- `RobustScaler` for numeric features
- `OneHotEncoder` for categorical features
### 4. Models Trained
9 classifiers trained with `GridSearchCV` (5-fold `StratifiedKFold`, scoring = F1):
 
| Model | Val F1 | Val Accuracy | Val AUC |
|---|---|---|---|
| **SVM (RBF)** ✅ | **0.894** | **0.870** | **0.927** |
| Random Forest | 0.886 | 0.857 | 0.931 |
| Gradient Boosting | 0.807 | 0.758 | 0.840 |
| KNN | 0.790 | 0.730 | 0.820 |
| Logistic Regression | 0.779 | 0.718 | 0.791 |
| AdaBoost | 0.772 | 0.691 | 0.746 |
| MLP | 0.763 | 0.694 | 0.755 |
| Decision Tree | 0.760 | 0.700 | 0.732 |
| Naive Bayes | ⚠️ invalid | ⚠️ invalid | 0.732 |
 
> ⚠️ Naive Bayes results are unreliable — `GaussianNB` assumes normally distributed features, which is violated after one-hot encoding categorical variables.
 
### 5. Winner Selection
**SVM with RBF kernel** was selected as the final model — highest F1 (0.894) and accuracy (0.870). While Random Forest had a marginally higher AUC (0.931 vs 0.927), the difference is negligible and F1 is the more relevant metric for binary classification.
 
### 6. Final Predictions
The winning model was refit on all 3,095 labeled rows (train + validation combined) before predicting on the test set.
 
| Model | Retained (1) | Churned (0) | Total |
|---|---|---|---|
| SVM (submitted) | 296 → 62.1% | 181 → 37.9% | 477 |
| Random Forest | 435 → 69.0% | 195 → 31.0% | 630 |
 
---
 
## 🔍 Key Findings
 
### Top 5 Features Driving Retention (Random Forest importance)
1. **Full Payment Participants (FPP) — 0.042** — more fully-paying students = stronger commitment
2. **Active Cancellation Insurance (FRP_Active) — 0.042** — buying insurance signals trust in the agency
3. **Total Passengers (Total_Pax) — 0.042** — larger groups are significantly more loyal
4. **Total School Enrollment — 0.041** — bigger schools → bigger groups → more loyal
5. **Days System to Departure — 0.039** — schools that plan earlier churn significantly less
### Loyal vs At-Risk School Profiles
 
| | Loyal School | At-Risk School |
|---|---|---|
| Group size | Large | Small |
| School size | Big | Smaller |
| Planning | ~400 days ahead | ~200 days ahead |
| Insurance | Buys it | Skips it |
| Participation rate | High | Low |
 
---
 
## 💡 Business Recommendations
 
### For Loyal Schools — Retain & Reward
- **Referral program** — reward large groups for bringing new schools
- **Personalized packages** — customize trips based on previous preferences
- **Early access** — give loyal schools first pick of dates and destinations
- **Loyalty program** — exclusive perks and returning customer discounts
- **VIP relationship** — dedicated account manager for top schools
### For At-Risk Schools — Intervene & Re-engage
- **Group growth rewards** — better pricing if they bring more students
- **Targeted packages** — smaller, more affordable group packages
- **Early booking incentives** — discounts for committing far in advance
- **Make insurance the default** — include cancellation insurance automatically
- **Proactive outreach** — flag at-risk schools early using the model
---
 
## ⚠️ Limitations
- **Single-year snapshot** — more historical data would improve predictions
- **Correlations only** — causation requires further study
- **Missing satisfaction data** — customer satisfaction surveys would add signal
- **Multicollinearity** — FPP, Total_Pax, FRP_Active are highly correlated, making individual feature ranking less robust
---
 
## 🛠️ Requirements
 
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```
 
---
 
