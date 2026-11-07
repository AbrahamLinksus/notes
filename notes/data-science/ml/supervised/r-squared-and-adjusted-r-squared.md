# R² and adjusted R²

> R² measures how much better a regression fits than just predicting the mean, and adjusted R² penalises predictors that don't earn their place.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 10–11)

## Key ideas
- **R² (coefficient of determination)** tells you how good the model is:
  `R² = 1 − SS_res / SS_total = 1 − Σ(yᵢ − ŷᵢ)² / Σ(yᵢ − ȳ)²`
  - SS_res = sum of squared differences between predicted and actual values.
  - SS_total = sum of squared differences between actual values and their **mean**.
- A properly fitted model lands between **0 and 1**. Closer to 1 = better.
- When SS_res > SS_total, R² goes **negative**. The model is worse than predicting the mean.
- **Adjusted R²**:
  `R²_adj = 1 − (1 − R²)(N − 1) / (N − P − 1)`, where N = samples and P = predictors.
  - It **penalises the number of predictors**. It falls when you add predictors that don't meaningfully improve the fit.

## Example
```
y     = [3, 5, 7]          ȳ = 5
ŷ     = [2.5, 5, 7.5]
SS_res   = 0.25 + 0 + 0.25 = 0.5
SS_total = 4 + 0 + 4       = 8
R² = 1 − 0.5/8 = 0.9375
```

## Pitfalls
- Plain R² never drops when you add a feature, even a useless one. Compare models with different feature counts using adjusted R².
- A negative R² isn't a calculation bug. It means the model is genuinely worse than the mean.
- A high R² doesn't mean the model is right. It can still be overfit or break the linear-regression assumptions.

## Related
- [Linear regression](linear-regression.md)
- [Classification metrics](classification-metrics.md)
- [Central tendency and dispersion](../../statistics/descriptive/central-tendency-and-dispersion.md)
