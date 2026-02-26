# Replication: Angrist & Evans (1998) — Children and Parental Labor Supply

## Track
**Track B: The Endogeneity & IV Strategy Track (Instrumental Variables)**

## Paper
Angrist, J. D., & Evans, W. N. (1998). Children and Their Parents' Labor Supply: 
Evidence from Exogenous Variation in Family Size. 
*American Economic Review*, 88(3), 450–477.

## Causal Question
Does having more children causally reduce parental labor supply (hours worked / earnings)?
Because family size is a choice (endogenous), the authors instrument for it using the 
sex composition of the first two children — parents are more likely to have a third child 
if the first two are the same sex, a preference unrelated to labor market outcomes.

## Data Source
Downloaded from the Angrist Data Archive at MIT Economics:
https://economics.mit.edu/people/faculty/josh-angrist/angrist-data-archive

The raw file (`census80.sas7bdat`) is not committed to this repo due to file size.
To replicate: download `census80.sas7bdat` from the link above and place it in `data/raw/`.

## Repository Structure
```
data/raw/          # Raw data files (not tracked by Git — see above)
notebooks/         # Analysis notebooks
  01_Data_Cleaning.ipynb
```

## Environment
- Python 3.10+
- pandas, pyreadstat, numpy, jupyter
