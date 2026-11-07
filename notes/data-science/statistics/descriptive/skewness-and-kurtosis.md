# Skewness and kurtosis

> Skewness measures how lopsided a distribution is, which shows up as the gap between mean and median, and kurtosis measures how heavy its tails are compared with its centre.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 4–5)

## Key ideas
- **Skew**: a measure of the asymmetry of a distribution.
  - **Right / positive skew**: mean > median. Outliers on the right drag the mean up.
  - **Left / negative skew**: mean < median.
  - **Symmetric**: mean ≈ median.
- **Kurtosis**: a statistical measure of the shape of a distribution's **tails relative to its centre**.
  - **Leptokurtic** (high kurtosis): extreme outliers, a high peak, long heavy tails.
  - **Mesokurtic** (normal): matches the normal bell curve. Kurtosis = 3, **excess kurtosis = 0**.
  - **Platykurtic** (low kurtosis): flat peak, short tails.

## Example
```
right skew          symmetric          left skew
  │█                    ▄█▄                   █│
  │██▄                 ▄███▄               ▄██ │
  │████▄▄___        ▄▄███████▄▄      ___▄▄████ │
   mode<median<mean  mean≈median   mean<median<mode

leptokurtic   │   mesokurtic   │   platykurtic
   tall spike │   bell curve   │   flat plateau
   heavy tails│   kurt = 3     │   thin tails
```
Salaries are right-skewed: a few huge earners pull the mean above the median.

## Pitfalls
- Skew direction follows the **tail**, not the peak. A right-skewed distribution has its peak on the left.
- Some tools report excess kurtosis (normal = 0) and some report raw kurtosis (normal = 3). Check which one you're looking at.
- With skewed data, use IQR to find outliers, not z-scores.

## Related
- [Central tendency and dispersion](central-tendency-and-dispersion.md)
- [Percentiles and outliers](percentiles-and-outliers.md)
- [Common distributions](../probability/common-distributions.md)
