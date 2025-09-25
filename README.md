
# Volatility Forecasting with GARCH Models

This project implements and compares **GARCH-family models** for volatility forecasting using daily WTI crude oil spot prices. The workflow moves from raw data acquisition to model evaluation, demonstrating both technical rigor and practical intuition.

---

## 1. Project Objective

The goal is to model and forecast financial market volatility using **GARCH(1,1)** and **EGARCH(1,1)** specifications.
Key aims:

* Identify volatility clustering in daily returns.
* Estimate conditional volatility models under realistic distributional assumptions.
* Compare models using out-of-sample forecast accuracy.
* Interpret persistence, asymmetry, and fat-tail effects.

---

## 2. Data

* **Source:** FRED (Federal Reserve Bank of St. Louis).
* **Asset:** Daily WTI crude oil spot price (`DCOILWTICO`).
* **Period:** 2000–present (daily frequency).
* **Transformation:** Log returns in percentage terms.

---

## 3. Methodology

1. **Exploratory Data Analysis**

   * Visualize prices and log returns.
   * Identify volatility clustering.
   * Summarize descriptive statistics.

2. **Statistical Testing**

   * Run **ARCH LM tests** on squared returns.
   * Confirm significant conditional heteroskedasticity.

3. **Model Estimation**

   * Fit **GARCH(1,1)** with Student-t innovations.
   * Fit **EGARCH(1,1)** with Student-t innovations and leverage term.
   * Evaluate parameters: persistence (α + β, β), shock response (α), asymmetry (γ), and heavy tails (ν).

4. **Diagnostics**

   * Check standardized residuals for whiteness.
   * Run Ljung–Box tests on squared residuals.

5. **Forecasting & Evaluation**

   * Generate 1-day-ahead rolling forecasts for last 252 days.
   * Compare against realized volatility proxies: |r| and 5-day realized variance (RV5).
   * Metrics: MSE, MAE, correlation, and QLIKE.

---

## 4. Results

* **GARCH(1,1):**

  * Persistence (α + β ≈ 0.985) indicates volatility shocks decay slowly.
  * Student-t ν ≈ 6.6 confirms fat tails.
  * Out-of-sample forecasts outperform EGARCH across all metrics.

* **EGARCH(1,1) with leverage:**

  * Persistence (β ≈ 0.986, α ≈ 0.139).
  * Leverage parameter γ ≈ –0.054 (significant): negative shocks raise volatility more than positive shocks.
  * Slightly weaker forecast performance than GARCH, though diagnostics confirm asymmetry is captured.

---

## 5. Conclusion

* **Main finding:** A parsimonious **GARCH(1,1) with Student-t errors** provided the best out-of-sample volatility forecasts for WTI crude oil.
* **Additional insight:** EGARCH reveals the expected **leverage effect**, but forecast metrics favored the simpler GARCH specification.
* **Implication:** Even basic GARCH models are powerful tools for risk management, though asymmetry should be tested for equity and commodity series.

---

## 6. Tools & Libraries

* Python (Jupyter Notebook)
* `pandas`, `numpy`, `matplotlib`
* `pandas_datareader` for FRED data
* `statsmodels` for ARCH LM tests and diagnostics
* `arch` for GARCH-family estimation and forecasting

