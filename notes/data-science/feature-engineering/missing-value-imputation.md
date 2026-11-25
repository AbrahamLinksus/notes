# Missing value imputation methods

> There are six ways to fill missing values, and mean/median/mode imputation assumes the data is MCAR.

studied: 2026-11-25 · status: done · source: Data_Boring.pdf (pp. 1, 11)

## Key ideas
- Methods listed:
  - impute with **mean / median / mode**
  - **random sample imputation**
  - **capture NaN with a new feature** (a flag column for "was missing")
  - **end of distribution** imputation
  - **arbitrary value** imputation
  - **frequent category** imputation (for categoricals)
- **Central-tendency imputation**:
  - assumes the data is **MCAR**
  - replaces with the most frequent occurrence, or the mean/median
- Measures of central tendency are the basis of the simplest fixes.

## Example
```python
df["age"] = df["age"].fillna(df["age"].median())
df["city"] = df["city"].fillna(df["city"].mode()[0])

df["age_missing"] = df["age"].isna()   # capture NaN as a new feature
```

## Pitfalls
- Mean/median/mode imputation is only justified under MCAR.
- Filling without a flag column loses the information that the value was missing.

## Related
- [Types of missing data](types-of-missing-data.md)
- [Central tendency and dispersion](../statistics/descriptive/central-tendency-and-dispersion.md)
- [Feature engineering steps](feature-engineering-steps.md)
