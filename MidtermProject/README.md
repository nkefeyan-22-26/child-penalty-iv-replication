# Replication: Angrist & Evans (1998) — Children and Parental Labor Supply

## Track
**Track B: The Endogeneity & IV Strategy Track (Instrumental Variables)**

## Paper
Angrist, J. D., & Evans, W. N. (1998). Children and Their Parents' Labor Supply:
Evidence from Exogenous Variation in Family Size.
*American Economic Review*, 88(3), 450–477.

## Causal Question
Does having more children causally reduce parental labor supply (hours worked / earnings)?
Because family size is a choice (endogenous), the authors instrument for it using the sex
composition of the first two children — parents are more likely to have a third child if the
first two are the same sex, a preference unrelated to labor market outcomes.

## Key Results

### Core IV Estimates
| Method | Coefficient on `morekids` | Interpretation |
|---|---|---|
| OLS (Biased) | — | Endogenous — not reliable |
| First Stage F-stat | 23,961 | Instrument is strong (>> 10) |
| Manual 2SLS | -16.59 weeks | Correct coef, wrong SEs |
| IV-2SLS (linearmodels) | -16.59 weeks | Correct coef + robust SEs |
| Wald Estimator | -14.58 weeks | No-controls raw IV estimate |

Having more than two children causally reduces a mother's weeks worked by approximately
16.6 weeks per year, identified using same-sex sibling composition as an instrument.

### Heterogeneous Treatment Effects by Race
| Race | Mothers (weeks) | Fathers (weeks) | Fathers Significant? |
|---|---|---|---|
| White | -17.47 | +2.07 | No |
| Black | -10.63 | +2.05 | No |
| Other | -9.88 | +1.38 | No |

The child penalty is large and statistically significant for mothers across all race groups,
but effectively zero for fathers regardless of race. White mothers face nearly twice the
penalty of Black and Other mothers, consistent with documented differences in labor force
attachment in 1980. The asymmetry between mothers and fathers holds universally.

## Data Source
Downloaded from the Angrist Data Archive at MIT Economics:
https://economics.mit.edu/people/faculty/josh-angrist/angrist-data-archive

The original file (`m_d_806.sas7bdat`) is a SAS binary format common in academic economics
research. It was loaded into Python, decoded from byte-string encoding, optimized, and saved
as compressed `.csv.gz` files. See `data/raw/README.md` for full documentation.

## Repository Structure
```
data/
└── raw/
    ├── README.md                          # Data documentation
    ├── census80_slim.csv.gz               # 20 key variables — used in all notebooks
    ├── census80_full.csv.gz               # All 85 variables — for reference
    └── notebooks/
        ├── 01_Data_Cleaning.ipynb         # Data ingestion, decoding, and processing
        ├── 02_Replication_Analysis.ipynb  # IV replication: First Stage, 2SLS, Wald
        └── 03_Extension_Analysis.ipynb    # HTE by race, mothers vs. fathers forest plots
```

## Reproducing the Analysis
1. Clone this repository
2. Download `m_d_806.sas7bdat` from the Angrist Data Archive and place it in `data/raw/`
3. Run `01_Data_Cleaning.ipynb` to reproduce the processed `.csv.gz` files
4. Run `02_Replication_Analysis.ipynb` to reproduce all IV results

## Environment
- Python 3.10+
- pandas, numpy, statsmodels, linearmodels, matplotlib, jupyter
```
