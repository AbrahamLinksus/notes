# Types of missing data: MCAR, MAR, MNAR

> The type of missingness (random, explained by other columns, or explained by the value itself) decides which fix is safe.

studied: 2026-11-25 · status: done · source: Data_Boring.pdf (p. 10)

## Key ideas
- Missing data can be **continuous** or **categorical**.
- **MCAR** (Missing Completely At Random):
  - no relationship between the missing data and other values
  - the probability of being missing is the same for all observations
  - e.g. wifi dropped at the moment of the weigh-in
- **MNAR** (Missing Not At Random):
  - also called systematic missing values
  - the missingness relates to the missing value itself
  - e.g. weight missing because of self-consciousness about weight
- **MAR** (Missing At Random):
  - missing data is systematic, but fully explained by other observed data
  - e.g. weight missing because the person was occupied

## Example
Weight column with blanks:
```
wifi dropped            → MCAR
person felt self-conscious → MNAR
person was occupied (explained by another column) → MAR
```

## Pitfalls
- The names are confusing: MAR is **not** the same as MCAR, because MAR missingness depends on other observed data.
- Simple central-tendency imputation assumes MCAR, so it is risky for MAR and MNAR.

## Related
- [Missing value imputation](missing-value-imputation.md)
- [Random forest: missing data](../ml/ensembles/random-forest-missing-data.md)
- [DS lifecycle and data analysis](ds-lifecycle-and-data-analysis.md)
