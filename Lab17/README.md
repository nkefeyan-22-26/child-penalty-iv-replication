# NY Fed Yield Curve Recession Model Replication

## Objective
Replicated the Federal Reserve Bank of New York's yield curve recession forecasting model by fitting a logistic regression on FRED macroeconomic data, demonstrating the theoretical and empirical superiority of the logit specification over the Linear Probability Model for binary recession prediction.

---

## Methodology

- **Data acquisition:** Retrieved two FRED series via the `fredapi` client — `T10Y3M` (10-Year minus 3-Month Treasury yield spread, daily) and `USREC` (NBER recession indicator, monthly) — covering January 1970 to present. Daily spread observations were resampled to month-end and lagged 12 months to align with the NY Fed's standard forecast horizon.

- **Baseline comparison — Linear Probability Model (LPM):** Estimated an OLS regression of the recession indicator on the lagged yield spread using `sklearn.LinearRegression` as a diagnostic baseline. Confirmed the canonical failure mode of the LPM on real data: fitted values outside the [0, 1] probability range, violating the axiomatic bounds of a probability measure.

- **Logistic regression:** Fitted a logistic regression (`sklearn.LogisticRegression`) of the NBER recession binary on the 12-month lagged spread, producing well-bounded sigmoid probabilities across the full covariate range. Validated coefficient stability using `TimeSeriesSplit` cross-validation to respect the temporal ordering of observations and prevent look-ahead leakage.

- **Statistical inference:** Re-estimated the model in `statsmodels.Logit` to extract maximum likelihood standard errors, computing the yield spread **odds ratio** and its **95% confidence interval** via exponentiation of the coefficient and Wald bounds — directly comparable to the published NY Fed model output.

- **Recession probability time series:** Generated the full fitted probability series from 1970 to present and annotated it with NBER recession shading. Examined the contested **2022–2024 inversion episode** in detail, during which the model produced elevated recession probabilities despite the absence of a subsequent NBER-designated contraction.

---

## Key Findings

**LPM vs. Logit — the case for the S-curve.** The Linear Probability Model produced predicted recession probabilities as low as −0.08 and as high as 1.14 on out-of-sample months, rendering its outputs uninterpretable as probabilities. The logistic specification constrained all predictions to (0, 1) and produced a well-identified sigmoid curve consistent with the economic prior that recession risk rises nonlinearly as the spread turns negative.

**Yield spread odds ratio.** The estimated odds ratio on the 12-month lagged T10Y3M spread was less than 1.0, confirming that a one-percentage-point *decline* in the spread (toward or through inversion) is associated with a statistically significant increase in the odds of recession 12 months ahead. The 95% confidence interval excluded 1.0, establishing the predictor's significance at conventional levels.

**2022–2024 inversion — elevated signal, no recession.** The model assigned recession probabilities well above the NY Fed's informal 30% warning threshold throughout the 2022–2024 inversion period — one of the deepest and most sustained T10Y3M inversions on record. No NBER recession was declared through mid-2024, contributing to an ongoing academic and policy debate about whether structural changes in the term premium (e.g., QT, post-pandemic yield dynamics) have altered the predictive content of this spread. This replication treats the episode as a genuine out-of-sample stress test: the model behaved as specified; whether the signal was correct remains an open empirical question.

---

## Stack
`Python` · `pandas` · `numpy` · `scikit-learn` · `statsmodels` · `matplotlib` · `fredapi`

## Data Sources
- [FRED T10Y3M](https://fred.stlouisfed.org/series/T10Y3M) — 10-Year Treasury Constant Maturity Minus 3-Month Treasury Constant Maturity
- [FRED USREC](https://fred.stlouisfed.org/series/USREC) — NBER-based Recession Indicators for the United States
- [NY Fed Reference Model](https://www.newyorkfed.org/research/capital_markets/ycfaq) — Federal Reserve Bank of New York Yield Curve as a Leading Indicator
