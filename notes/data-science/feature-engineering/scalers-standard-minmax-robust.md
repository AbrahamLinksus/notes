# Scalers: StandardScaler, MinMaxScaler, RobustScaler

> Pick the scaler by the data: standardization for features on very different ranges, min-max for images and neural nets, robust scaling when outliers are heavy.

studied: 2026-11-25 · status: done · source: Data_Boring.pdf (p. 3)

## Key ideas
- **Why transform**: convert raw data into a format that better meets the statistical assumptions of ML algorithms, improving accuracy and speed.
- **Standardization** (`StandardScaler`):
  - use when features have large range differences or different units
  - `z = (x − mean) / std`, giving mean = 0 and std = 1
  - centres the data on its mean and scales by its variability
- **Normalization** (`MinMaxScaler`):
  - squeezes every feature into 0–1
  - `x' = (x − x_min) / (x_max − x_min)`
  - best use cases: images, neural networks
- **Robust scaler** (`RobustScaler`):
  - scales using the median and quantiles
  - `x' = (x − median) / IQR`
  - resilient to outliers, so best for data with heavy outliers

## Example
```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler, RobustScaler

StandardScaler().fit_transform(df[["salary"]])   # mean 0, std 1
MinMaxScaler().fit_transform(df[["pixel"]])      # 0 to 1
RobustScaler().fit_transform(df[["income"]])     # median/IQR based
```

## Pitfalls
- Min-max uses the min and max, so a single outlier squashes everything else. Use the robust scaler when outliers are heavy.
- Normalization and standardization are different things, even though people mix up the names.

## Related
- [Feature engineering steps](feature-engineering-steps.md)
- [Outlier sensitivity by model](outlier-sensitivity-by-model.md)
- [Z-score and standard normal](../statistics/probability/z-score-and-standard-normal.md)
