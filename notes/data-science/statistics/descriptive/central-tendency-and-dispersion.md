# Central tendency and dispersion

> Mean, median and mode tell you where the data sits, and range, IQR, variance and SD tell you how spread out it is. With outliers, prefer median and IQR.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 4, 47)

## Key ideas
- **Central tendency**:
  - **Mean** = sum of all values / count, the "average". **Prone to outliers.**
  - **Median** = middle value once sorted. **Insensitive to the tails.**
  - **Mode** = most frequent value.
  - Outliers skew the mean. The median stays put.
- **Dispersion (spread)** shows how the data is distributed:
  1. **Range** = max − min.
  2. **IQR** = Q3 − Q1 (75th percentile − 25th), the range of the middle 50%. Best for **skewed data**.
  3. **Variance** = Σ(x − μ)² / N, how spread out the values are.
  4. **Standard deviation** σ = √variance, how far the values typically sit from the mean.
  5. **Mean deviation**.

## Example
Data: 2, 3, 3, 4, 100

```
mean   = 112/5 = 22.4     ← dragged up by 100
median = 3                ← unaffected
mode   = 3
range  = 98
```
Without the 100: mean = 3, which matches the median. One outlier moved the mean by 19.

## Pitfalls
- Reporting the mean on skewed data (income, house prices) is misleading. Use the median.
- Variance is in squared units. SD brings it back to the data's units, so quote SD.
- The range uses only two values, so a single outlier wrecks it. IQR is robust.

## Related
- [Skewness and kurtosis](skewness-and-kurtosis.md)
- [Percentiles and outliers](percentiles-and-outliers.md)
- [Types of data and statistics](types-of-data-and-statistics.md)
- [Z-score and standard normal](../probability/z-score-and-standard-normal.md)
