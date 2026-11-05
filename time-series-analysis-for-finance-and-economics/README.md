# 📈 Time Series Analysis with Gretl: Solar Energy Forecasting and Stock Volatility

**Course:** Time Series Analysis for Finance and Economics  
**Institution:** Politecnico di Milano – Graduate School of Management  
**Team:** Luca Stucchi, Stole Donev, Tiziano Gallo

---

## 📌 Overview

An applied econometrics report in two parts, both built in **Gretl**. The first forecasts U.S. solar electricity generation and tests whether natural gas generation and electricity prices help predict it. The second models the volatility of a large renewable energy stock, NextEra Energy (NEE), and produces a one-day-ahead volatility forecast.

---

## ☀️ Problem 1: Forecasting Energy Variables

**Data:** U.S. monthly net solar electricity generation (MkWh) from the EIA, January 2011 to December 2024 (168 observations). Output grew from 37 MkWh to 24,483 MkWh, with clear seasonality, so the series is log-transformed. Natural gas net generation and retail electricity price (cents/kWh) are added as log-transformed series for the multivariate model.

**Approach:**
1. Split the data into training (144 months) and test (24 months) sets.
2. Estimate ARMA(p, q) models for p, q from 0 to 4 on ln(Solar), with a constant, a linear time trend and 11 monthly seasonal dummies, and rank them by BIC.
3. Check the residual ACF and PACF, then forecast.
4. Estimate a VAR(2) with solar, natural gas and electricity price, test for Granger causality, and compare its forecasts with the univariate model.

**Results:**

| Item | Result |
|---|---|
| Best model by BIC | AR(2), BIC = −211.61 |
| Test-period forecast accuracy (Jan 2023 to Dec 2024) | RMSE = 0.044, Theil's U2 = 0.240 |
| Out-of-sample forecast (Jan 2025 to Dec 2026) | June 2026 ≈ 10.49 log units, about 36,000 MkWh |
| VAR(2) fit | R² = 0.996 (solar), 0.973 (gas), 0.987 (price) |
| Granger causality | Solar generation is not caused by gas or price, and no significant link between gas and solar |
| VAR(2) vs AR(2) forecasts | Maximum gap of about 0.05 log units, so the VAR adds no accuracy and AR(2) is kept |

**Caveat:** The fitted AR(2) is technically non-stationary, because its coefficients sum to almost 1. The report attributes this to the explosive growth in solar output, and also notes small residual autocorrelation at lags 8 and 18.

---

## 📉 Problem 2: Modelling Volatility

**Data:** Daily adjusted closing prices of NextEra Energy (NEE), the largest U.S. renewable energy utility, from Yahoo Finance, 11 May 2022 to 10 May 2026 (1,002 observations).

**Approach:**
1. Compute daily log-returns and summary statistics.
2. Test for ARCH effects in squared returns.
3. Estimate a GARCH(1,1) model and check its residuals.
4. Forecast volatility one day ahead.

**Results:**

| Item | Result |
|---|---|
| Daily log-returns | Mean 0.039%, standard deviation 1.727% |
| Annualised volatility (full sample) | 27.41% |
| ARCH effects | Engle ARCH-LM (5 lags) = 31.88, p < 0.001, so volatility clustering is confirmed |
| GARCH(1,1) | All variance parameters significant, likelihood ratio χ²(2) = 37.74, p < 0.001 |
| Residual diagnostics | Ljung-Box Q(30) = 14.51, p = 0.992, so no remaining ARCH effects |
| One-day-ahead forecast (11 May 2026) | Daily volatility 1.63%, about 25.93% annualised |
| 95% forecast interval for next-day return | −3.17% to +3.23% |

**Caveat:** The estimated volatility persistence is low, and the report notes that a regime-switching model or a longer sample could fit better, given the turbulent 2022 to 2023 period followed by calmer 2024 to 2025.

---

## 🔬 Methods

- ARMA model selection with BIC
- Trend and seasonal dummy regression
- Out-of-sample forecast evaluation (RMSE, Theil's U2)
- Vector autoregression (VAR) and Granger causality
- Ljung-Box and Portmanteau tests
- ARCH-LM test and GARCH(1,1) volatility modelling

---

## 📄 Deliverable

[`Time_Series_Report_Stucchi_Donev_Gallo.pdf`](Time_Series_Report_Stucchi_Donev_Gallo.pdf): the full 10-page report, with figures, tables and an appendix of Gretl output.

---

## 🛠️ Tools & Technologies

![Gretl](https://img.shields.io/badge/Gretl-Econometrics-1F6FB2)
