# The Architecture of Dimensionality: Hedonic Pricing & the FWL Theorem

---

## Objective

Executed a multivariate hedonic pricing model on 2026 California real estate data to empirically demonstrate the Frisch-Waugh-Lovell (FWL) theorem — proving that partial regression via sequential residualization produces a coefficient mathematically identical to its full multivariate OLS counterpart.

---

## Dataset

| Field | Description | Source |
|---|---|---|
| `Sale_Price` | Residential transaction price (USD) | Zillow Synthetic (2026) |
| `Property_Age` | Age of structure at time of sale (years) | Zillow Synthetic (2026) |
| `Distance_to_Tech_Hub` | Euclidean proximity to nearest major tech employment center (km) | Zillow Synthetic (2026) |

> **Environment:** Python 3.10+ · pandas · statsmodels.formula.api · matplotlib

---

## Methodology

**Stage 1 — Baseline Multivariate OLS (Full Model)**
- Estimated a hedonic pricing regression of the form:  
  `Sale_Price ~ Property_Age + Distance_to_Tech_Hub`
- Extracted the multivariate coefficient β₁ for `Property_Age` as the benchmark — the ceteris paribus partial effect with `Distance_to_Tech_Hub` held constant.

**Stage 2 — Omitted Variable Bias (OVB) Demonstration**
- Re-estimated a restricted univariate model deliberately omitting `Distance_to_Tech_Hub`:  
  `Sale_Price ~ Property_Age`
- Documented the directional and magnitude shift in β₁, quantifying the degree of OVB introduced by the excluded regressor.

**Stage 3 — Manual FWL Residualization (Partialling Out)**
- Regressed `Property_Age` on `Distance_to_Tech_Hub` and extracted the residuals **ẽ_Age** — the component of `Property_Age` orthogonal to (unexplained by) `Distance_to_Tech_Hub`.
- Regressed `Sale_Price` on `Distance_to_Tech_Hub` and extracted the residuals **ẽ_Price** — the component of `Sale_Price` not explained by `Distance_to_Tech_Hub`.
- Regressed **ẽ_Price** on **ẽ_Age**, recovering the FWL partial coefficient for `Property_Age` through pure residual space.

**Stage 4 — Algebraic Verification**
- Confirmed a floating-point-exact match between the FWL-derived coefficient and the Stage 1 multivariate coefficient, validating the theorem computationally.

---

## Key Findings

### Omitted Variable Bias
Omitting `Distance_to_Tech_Hub` from the model produced a severely biased estimate of `Property_Age`'s effect on sale price. Because older properties in the California dataset are disproportionately located farther from major tech employment centers — and distance itself is a strong negative predictor of price — the univariate model incorrectly attributed a portion of the distance penalty to the physical age of the structure. The result was an inflated (in absolute magnitude) and directionally misleading coefficient on `Property_Age` that confounded spatial depreciation with structural depreciation.

### FWL Theorem as Algorithmic Ceteris Paribus
Manual residualization successfully decomposed the shared covariance between `Property_Age` and `Distance_to_Tech_Hub`, isolating the net variation in each variable that is linearly independent of the other. Regressing the purged residuals against one another recovered a coefficient for `Property_Age` in exact numerical agreement with the full multivariate OLS estimate — demonstrating that multivariate OLS does not simply "add controls," but rather mechanically partials out all inter-regressor covariance before estimating each marginal effect. The FWL theorem thus provides a rigorous geometric and algebraic proof that OLS achieves ceteris paribus estimation through sequential orthogonal projection onto residual subspaces.

---

## Implications

This lab operationalizes a foundational result in econometric theory with direct applied relevance: coefficient estimates in any multivariate regression are only causally interpretable to the degree that the model's control set successfully absorbs confounding covariance. The FWL proof makes this mechanism explicit — what OLS reports as a partial effect is, by construction, the relationship that survives after the shared signal of all other regressors has been stripped away.

---

*Lab completed as part of an applied econometrics curriculum. Data: Zillow Synthetic California Real Estate Metrics (2026).*
