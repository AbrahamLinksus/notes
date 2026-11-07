# Percentiles, the five-number summary and outlier detection

> To flag outliers, use IQR fences (Q1 − 1.5·IQR, Q3 + 1.5·IQR) on skewed data and |z| > 3 on normal data, so check the shape of the distribution before picking a method.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 48, 54–55)

## Key ideas
- **Percentile**: the value below which a given percentage of the observations fall.
  `percentile of x = (number of values below x / n) × 100`
- **Five-number summary**: a quick view of the centre, spread and distribution:
  min, Q1, median, Q3, max.
- **IQR method**:
  - IQR = Q3 − Q1
  - lower fence = Q1 − 1.5·IQR, upper fence = Q3 + 1.5·IQR
  - Anything outside the fences is an outlier.
  - It's rank-based, so it works on **skewed** data.
- **Z-score method**:
  - z = (x − mean) / SD. Flag the point if **|z| > 3** (an empirical rule).
  - It **assumes a normal distribution**.

## Example
Data: 1, 2, 3, 4, 5, 6, 7, 8, 30

```
Q1 = 2.5, median = 5, Q3 = 7.5 → IQR = 5
lower fence = 2.5 − 7.5 = −5
upper fence = 7.5 + 7.5 = 15
→ 30 > 15 → outlier

five-number summary: 1, 2.5, 5, 7.5, 30
```

## Pitfalls
- On skewed data, z-scores mislead: the outliers inflate the SD and hide themselves.
- Different tools use slightly different quartile methods. Q1 and Q3 can differ a bit between them.
- The "1.5" and "3" cut-offs are conventions, not laws.

## Related
- [Central tendency and dispersion](central-tendency-and-dispersion.md)
- [Skewness and kurtosis](skewness-and-kurtosis.md)
- [Z-score and standard normal](../probability/z-score-and-standard-normal.md)
- [Feature engineering steps](../../feature-engineering/feature-engineering-steps.md)
