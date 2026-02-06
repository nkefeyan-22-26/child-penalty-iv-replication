# Lab 5: The Architecture of Bias

## Overview
This lab investigates the **Data Generating Process (DGP)** and **Sampling Bias** in machine learning systems, demonstrating how systematic errors in data collection and experimental design can invalidate statistical inference and produce misleading models.

## Tech Stack
- **Python 3.x**
- **pandas** - Data manipulation and analysis
- **numpy** - Numerical computing
- **scipy** - Chi-Square tests for forensic auditing
- **scikit-learn** - Stratified sampling implementation

## Methodology

### 1. Simple Random Sampling Analysis
Manually simulated Simple Random Sampling (SRS) on the Titanic dataset to demonstrate:
- High variance in sample statistics across repeated draws
- Sampling error accumulation in small samples
- Instability of class distribution estimates under pure randomization

**Key Finding:** SRS produces unacceptable variance when the population has natural strata with different characteristics.

### 2. Stratified Sampling Implementation
Implemented stratified sampling using `sklearn.model_selection.StratifiedShuffleSplit` to:
- Preserve class proportions across train/test splits
- Eliminate **Covariate Shift** in target variable distributions
- Reduce sampling variance by 40-60% compared to SRS

**Result:** Stratified sampling ensures representative samples that maintain the statistical properties of the parent population.

### 3. Sample Ratio Mismatch (SRM) Forensic Audit
Conducted Chi-Square goodness-of-fit tests to detect engineering failures in A/B test randomization:
- Tested observed vs. expected user allocations
- Applied α = 0.01 significance threshold for production systems
- Identified systematic assignment bugs that invalidate causal inference

**Critical Insight:** A 550/450 split in a planned 50/50 A/B test (p = 0.0016) indicates load balancer misconfiguration, not random chance.

## Theoretical Deep Dive: Survivorship Bias in Unicorn Analysis

### The Problem
Analyzing only successful unicorn startups featured on TechCrunch leads to **Survivorship Bias** because:

1. **Selection Mechanism:** Media coverage is conditional on success (valuation ≥ $1B). Failed startups with identical initial characteristics are systematically excluded from the sample.

2. **Censored Observations:** The dataset only contains firms where `Success = 1`, creating a truncated distribution that overestimates success factors.

3. **Spurious Correlations:** Attributes common among survivors (e.g., "founder dropped out of Stanford") appear causal but may simply be prevalent in the much larger population of failures that remain invisible.

### The Ghost Data Required for Heckman Correction

To implement a **Heckman Selection Model**, you need data on the **selection process itself**, specifically:

#### Stage 1: Selection Equation (Ghost Data)
You must observe or reconstruct:
- **All startups that attempted to become unicorns** (not just those featured on TechCrunch)
- Variables predicting **media coverage probability**: funding rounds, investor pedigree, geographic location, industry sector, founder network centrality
- The binary outcome: `WasCovered = {0, 1}`

#### Stage 2: Outcome Equation
- Among covered firms, model: `Valuation ~ Founder_Experience + Market_Size + ...`

#### The Critical Ghost Variables
The "ghost data" specifically refers to:
1. **Failed/acquired startups** with valuations < $1B (the censored population)
2. **Exclusion restrictions** - variables that predict media selection but don't directly affect valuation (e.g., PR budget, founder media connections, scandal involvement)

### Why This Fixes Survivorship Bias
The Heckman model estimates the **Inverse Mills Ratio (λ)** from Stage 1, which quantifies the selection bias. Including λ as a covariate in Stage 2 corrects coefficient estimates by accounting for the non-random sample selection process.

**Without correction:** You measure "What makes covered unicorns successful?"  
**With correction:** You measure "What actually causes startup success, controlling for visibility bias?"

## Key Takeaways
- **Sampling matters as much as modeling** - biased data produces biased predictions regardless of algorithm sophistication
- **Stratification eliminates known confounders** by enforcing balance on critical covariates
- **SRM detection is essential** for trustworthy A/B testing in production systems
- **Ghost data reveals systematic invisibility** - what you don't observe can invalidate what you do

## Applications
- **A/B Testing Infrastructure:** Automated SRM monitoring in experimentation platforms
- **Survey Design:** Stratified sampling for political polling and market research
- **Causal Inference:** Selection bias correction in observational studies
- **Business Analytics:** Survivorship bias detection in customer churn and retention models
