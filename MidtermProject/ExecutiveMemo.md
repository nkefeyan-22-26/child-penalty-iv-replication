# The Hidden Cost of Parenthood on Women's Careers

**To:** Policy Stakeholders
**From:** Nathan Kefeyan
**Re:** Causal Evidence on the Labor Market Impact of Family Size — Replication & Extension of Angrist & Evans (1998)
**Date:** March 2026

---

Having a third child causally reduces a mother's weeks worked by about 16.6 weeks per year (equal to four months of lost work), while having virtually zero measurable effect on fathers. This penalty is the largest for White mothers (-17.5 weeks) and about half as large for Black (-10.6 weeks) and Other (-9.9 weeks) mothers. This reveals that the burden of parenthood on careers is uneven depending on race and gender.

---

## Methodology

The biggest challenge in measuring the effect of children on careers is that family size is a choice. Women who choose to have more children may differ in ways that also affect their careers. They might be more ambitious, riskier, or have different financial or personal values. If we just compared mothers with two versus three children, the effect of the child would be confounded by these differences.

To solve this, we used an **Instrumental Variables (IV)** design, testing a random aspect: the sexes of the first two children. Parents who have two boys or two girls are significantly more likely to have a third child than parents who already have one of each. This shows families' preferences for mixed-sex households. Whether your first two children happen to be the same sex is random, so it has no direct effect on a mother's career trajectory.

This instrument is valid because:

1. Same-sex siblings strongly predict having a third child (F-statistic = 23,961, far above the accepted threshold of 10)
2. The sex of your first two children has no plausible direct effect on how many weeks per year you work, except through the channel of having an additional child

---

## Figure 1: IV-2SLS Estimates of the Child Penalty on Weeks Worked by Race and Parent Gender
![Child Penalty by Race: Mothers vs. Fathers](data/raw/notebooks/forest_plot_race.png.png)
![Child Penalty by Race: Mothers vs. Fathers](data/raw/notebooks/forest_plot_mothers_vs_fathers.png.png)

*Each dot represents the causal effect of having a third child on annual weeks worked for a given race-gender group. The instrument is the same-sex sibling composition. The lines show 95% confidence intervals. The red-dashed line marks zero (no effect).
Data: 1980 U.S. Census extract; Angrist & Evans (1998)*

The left panel shows that the child penalty in weeks reduced for mothers is large and significant across all three race groups, as confidence intervals are below zero. The right panel shows that fathers experience no statistically significant change in weeks worked, regardless of race (all confidence intervals are above zero).

---

## Policy Implications

1. **Parental leave policies are not gender neutral in practice** — the burden of additional children falls almost entirely on mothers. Assuming a shared burden between mothers and fathers is misaligned with this data.

2. **The racial gradient exposes a potential targeted intervention** — White mothers face a penalty nearly twice the size of Black and Other mothers, likely reflecting a structural difference. White mothers in this era were more able to exit the workforce entirely after a third child, while Black mothers had higher baseline labor force participation due to economic necessity. Workplace retention programs that focus on senior or high-earning women (skewed White) might have a harder time succeeding due to White women facing the highest penalty for a third child.

3. **The career tax on mothers is a structural outcome** — the relationship is causal rather than just correlational, telling us that the child causes the labor penalty and nothing else. This is addressable through policies like subsidized childcare, flexible scheduling, and onboarding programs for returning mothers. The expected return is a measurable positive effect on recovered labor supply.
