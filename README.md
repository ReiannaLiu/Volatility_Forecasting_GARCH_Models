# GARCH Volatility Forecasting on S&P 500

This project focuses on **modeling and forecasting volatility** of the S&P 500 index using the **GARCH(1,1) model**, and benchmarking its performance against simpler models like **Rolling Standard Deviation** and **EWMA (Exponentially Weighted Moving Average)**.

---

## **Project Overview**
Financial returns often show **volatility clustering** — periods of high volatility followed by high volatility, and calm periods followed by calm periods.  
To capture this, we:
1. Analyze daily S&P 500 returns,
2. Fit a **GARCH(1,1)** model to estimate conditional volatility,
3. Forecast future volatility (1-day and 30-day ahead),
4. Benchmark GARCH against **Rolling Std** and **EWMA** models.

---

## **Data**
- **Ticker:** `^GSPC` (S&P 500 Index).
- **Source:** Yahoo Finance (`yfinance` library).
- **Time Period:** 2015-01-01 to 2025-01-01.
- **Fields:** Adjusted close price, daily log returns.

---

## **Methodology**
1. **Data Preprocessing**
   - Downloaded daily S&P 500 data from `yfinance`.
   - Computed **log returns**:  
     $$
     r_t = \ln \frac{P_t}{P_{t-1}}
     $$

2. **Exploratory Data Analysis**
   - **Rolling Volatility (30-day):**  
     Visualized volatility clustering.
   - **ACF of Squared Returns:**  
     Confirmed persistence in volatility, supporting GARCH assumptions.

3. **Modeling**
   - **GARCH(1,1):** Estimated parameters $\omega, \alpha, \beta$.
   - Generated 1-day and 30-day volatility forecasts.

4. **Benchmark Models**
   - **Rolling Std (30-day window).**
   - **EWMA (λ = 0.94)** — RiskMetrics-style volatility estimate.

5. **Evaluation Metrics**
   - **MSE (Mean Squared Error).**
   - **QLIKE Loss (Quasi-Likelihood).**

---

## **Key Results**
- **GARCH(1,1) Parameters:**  
  $\alpha = 0.168$, $\beta = 0.799$, $\alpha + \beta = 0.967$ → **mean-reverting volatility**.

- **1-Day Forecast:** ~0.97% volatility.

- **Model Performance (last 250 days):**
  | Model             | MSE    | QLIKE  |
  |-------------------|--------|--------|
  | GARCH(1,1)        | 1.47   | 0.56   |
  | Rolling Std (30d) | 1.40   | 0.47   |
  | EWMA (λ=0.94)     | **1.29** | **0.38** |

- **Conclusion:**  
  **EWMA outperformed GARCH** in short-term forecasting, but GARCH remains valuable for theoretical modeling and longer-horizon forecasts.

---

## **Key Visualizations**
- **Daily Log Returns & Rolling Volatility.**
- **ACF of Squared Returns.**
- **Estimated Conditional Volatility (GARCH vs. Realized).**
- **Forecasted vs. Realized Volatility.**
- **Model Comparison (GARCH vs. EWMA vs. Rolling Std).**

---

## **Tech Stack**
- **Python 3.11**
- Libraries:
  - `yfinance` (data collection),
  - `pandas`, `numpy` (data analysis),
  - `matplotlib`, `seaborn` (visualization),
  - `arch` (GARCH modeling),
  - `statsmodels` (ACF plots),
  - `sklearn` (MSE metric).

---

## **Next Steps**

* Extend to **EGARCH / GJR-GARCH** models to capture asymmetry.
* Backtest **Value-at-Risk (VaR)** using GARCH volatility forecasts.
* Compare performance across multiple indices (e.g., Nasdaq, Dow Jones).