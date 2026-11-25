# Gaussian transformations

> Gaussian transformations turn non-normal data into a bell shape, which matters for models like linear regression that assume normally distributed data.

studied: 2026-11-25 · status: done · source: Data_Boring.pdf (pp. 4–5)

## Key ideas
- **Goal**: convert a non-normal distribution into a normal (bell-shaped) one.
- **Why**: models such as linear regression assume the data is normally distributed.
- Transformations covered:
  - **Logarithmic**: `x → log(x)`. Fixes **right-skewed** data.
  - **Reciprocal**: `x → 1/x`. Create a new column. Helps fix skewness, linearize data and fix heteroscedasticity.
  - **Square root**: `x → √x`.
  - **Exponential**: `x → e^x` (as written in the notes).
  - **Box-Cox**: `y(λ) = (Y^λ − 1) / λ`, a parameterised family where λ is chosen to make the data more normal.

## Example
```python
import numpy as np

df["income_log"] = np.log(df["income"])        # right-skewed → closer to bell
df["time_recip"] = 1 / df["time"]              # new column, original kept
```

## Pitfalls
- `log` and `1/x` break on zero or negative values, so check the range first.
- Reciprocal is applied into a **new column**, so don't overwrite the original.
- A transform that fixes skew in one direction can make a left-skewed column worse. Plot before and after.

## Related
- [Skewness and kurtosis](../statistics/descriptive/skewness-and-kurtosis.md)
- [Linear regression](../ml/supervised/linear-regression.md)
- [Scalers](scalers-standard-minmax-robust.md)
