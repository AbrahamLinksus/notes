# DS project lifecycle and what to check in data analysis

> A DS project runs from data collection to deployment, and the data-analysis stage is about understanding the data without changing it.

studied: 2026-11-25 · status: done · source: Data_Boring.pdf (pp. 1–2)

## Key ideas
- **Lifecycle**: data collection → data analysis → feature engineering → feature selection → model building → model deployment.
- **Data analysis** is for understanding, so the data is not modified at this stage.
- Things to check:
  - missing values
  - numeric values and their distributions
  - categorical variables and their **cardinality** (number of distinct categories)
  - outliers
  - the relationship between features and the outcome
- **EDA** (exploratory data analysis) covers numerical and categorical feature analysis, missing values, outliers and raw-data cleaning, using visualisation to explore.
- Feature engineering then handles missing values, imbalance, outliers, scaling and categorical-to-numerical conversion.
- Feature selection comes after, and has to deal with the curse of dimensionality.

## Example
```
collect → analyse (look, don't touch) → engineer (fix/transform)
        → select features → build model → deploy
```
Analysis finds that `age` has 8% missing and `income` is right-skewed. Engineering is where you impute `age` and transform `income`.

## Pitfalls
- Changing data while "just exploring" mixes up analysis and engineering, and you lose track of what was altered.
- High-cardinality categoricals are easy to miss until encoding blows up the column count.

## Related
- [Feature engineering steps](feature-engineering-steps.md)
- [Types of missing data](types-of-missing-data.md)
- [Scalers](scalers-standard-minmax-robust.md)
