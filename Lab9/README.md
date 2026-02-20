# Recovering Experimental Truths via Propensity Score Matching

## Objective
Demonstrate that principled causal inference methods can rehabilitate observational data corrupted by systematic selection bias, recovering treatment effect estimates that closely replicate those obtained from a randomized controlled trial.

## Methodology
- **Selection Bias Modeling:** Characterized the non-random assignment mechanism in the observational Lalonde dataset, identifying systematic differences in pre-treatment covariates between the treated and control groups that render naive comparisons invalid.
- **Propensity Score Estimation:** Fit a logistic regression model to estimate each unit's conditional probability of treatment assignment given observed covariates, collapsing the high-dimensional confounding structure into a single balancing score.
- **Nearest-Neighbor Matching:** Paired each treated unit to its closest control-group counterpart in propensity score space, constructing a matched sample in which covariate distributions are approximately balanced across treatment arms.
- **Treatment Effect Recovery:** Computed the Average Treatment Effect on the Treated (ATT) on the matched sample, benchmarking the result against both the naïve observational estimate and the known experimental ground truth.

## Key Findings

The naïve comparison of unmatched groups produced a wildly misleading estimate of **−$15,204**, reflecting the severe self-selection of lower-earning individuals into the job training program rather than any true causal effect.

After propensity score matching restored covariate balance, the recovered treatment effect converged to approximately **+$1,800** — closely tracking the experimental benchmark from the Lalonde RCT and confirming that the matching procedure successfully isolated the causal signal from selection noise.

| Estimator | Estimated Earnings Impact |
|---|---|
| Naïve (Unmatched) | −$15,204 |
| PSM – Nearest Neighbor (Matched) | **+$1,800** |
| Experimental Ground Truth (RCT) | ~+$1,800 |

> A swing of over **$17,000** in estimated program impact — eliminated through matching.

## Stack
Python · Pandas · Scikit-Learn
