# SMOTE: synthetic minority over-sampling

> SMOTE creates new synthetic minority samples by interpolating between existing minority points, instead of duplicating rows.

studied: 2026-11-25 · status: done · source: Data_Boring.pdf (p. 9)

## Key ideas
- Full name: **S**ynthetic **M**inority **O**ver-sampling **T**echnique.
- Regular over-sampling duplicates minority rows. SMOTE **generates synthetic samples** for the minority class instead.
- It uses **linear interpolation** between existing minority points to make the new ones.
- It lives in `imblearn`, like the other resamplers.

## Example
```
Minority points A=(1, 2) and B=(3, 6).
A synthetic point lies on the line between them, e.g. (2, 4).
```
```python
from imblearn.over_sampling import SMOTE
X_res, y_res = SMOTE().fit_resample(X, y)
```

## Pitfalls
- It interpolates, so new points always lie between existing minority points.
- It only creates minority samples. It doesn't fix other data-quality problems.

## Related
- [Handling imbalanced datasets](handling-imbalanced-data.md)
- [Feature engineering steps](feature-engineering-steps.md)
