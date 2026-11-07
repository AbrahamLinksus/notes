# Feature engineering steps

> Feature engineering turns raw data into useful data: EDA, then missing values, class imbalance, outliers, and finally scaling (normalisation or standardisation).

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 24, 57, 62)

## Key ideas
- Goal: **raw data → useful data** for the model.
- **Step 1, EDA**: visualise and inspect
  - numerical features
  - categorical features
  - missing values
  - outliers
  - then clean.
- **Step 2, handle missing values**: fill with the mean, median or mode.
- **Step 3, handle an imbalanced dataset**.
- **Step 4, treat outliers** (IQR fences or z-score).
- **Step 5, scale the data**:
  - **Normalisation** scales into the range **0–1**.
  - **Standardisation** centres on mean **0** with SD **1** (z-score).
- Whether you need scaling depends on the model:
  - **KNN**: normalisation is highly required, because it's distance-based.
  - **Random forest**: not required, because splits are threshold rules and scale doesn't affect them.

## Example
```python
import pandas as pd
from sklearn.preprocessing import MinMaxScaler, StandardScaler

df["age"] = df["age"].fillna(df["age"].median())        # step 2

q1, q3 = df["income"].quantile([.25, .75]); iqr = q3 - q1  # step 4
df = df[df["income"].between(q1 - 1.5*iqr, q3 + 1.5*iqr)]

df[["age"]]    = MinMaxScaler().fit_transform(df[["age"]])     # 0–1
df[["income"]] = StandardScaler().fit_transform(df[["income"]])  # μ0 σ1
```

## Pitfalls
- Fit scalers and imputers on the **train** split only, then apply them to test. Fitting on all the data leaks test information.
- Mean imputation is distorted by outliers. Use the median on skewed features.
- Normalisation and standardisation aren't the same thing. Pick based on the model and the data's shape.

## Related
- [Percentiles and outliers](../statistics/descriptive/percentiles-and-outliers.md)
- [Z-score and standard normal](../statistics/probability/z-score-and-standard-normal.md)
- [K-nearest neighbours](../ml/supervised/k-nearest-neighbours.md)
- [Random forest](../ml/ensembles/random-forest.md)
- [Random forest: missing data](../ml/ensembles/random-forest-missing-data.md)
