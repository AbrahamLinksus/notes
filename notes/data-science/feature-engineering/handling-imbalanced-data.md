# Handling imbalanced datasets: class weights, under- and over-sampling

> For imbalanced classes you either weight the classes, cut the majority (loses data), or grow the minority (usually better).

studied: 2026-11-25 · status: done · source: Data_Boring.pdf (pp. 8–9)

## Key ideas
- An **imbalanced dataset** has classes or categories that are not represented equally.
- **Class weights**: tell the model to give more importance to a specific class.
  - `{0: 1, 1: 1}` means equal preference.
  - `{0: 1, 1: 100}` gives the minority class far more preference.
- **Under-sampling**: reduce the majority-class points to balance.
  - Downside: a huge loss of data from the majority class.
  - Done with `NearMiss()` from `imblearn`.
- **Over-sampling**: increase the minority-class examples so the model can learn the rare cases.
  - Usually better than under-sampling.
  - Done with `RandomOverSampler()` from `imblearn`, which duplicates minority rows.
  - [SMOTE](smote.md) is the synthetic alternative.

## Example
```python
from imblearn.under_sampling import NearMiss
from imblearn.over_sampling import RandomOverSampler

X_u, y_u = NearMiss().fit_resample(X, y)            # shrink majority
X_o, y_o = RandomOverSampler().fit_resample(X, y)   # duplicate minority
# or: LogisticRegression(class_weight={0: 1, 1: 100})
```

## Pitfalls
- Under-sampling throws away majority information.
- Plain random over-sampling copies rows, so the model sees exact duplicates.
- Accuracy is misleading on imbalanced data. Check precision, recall and AUC.

## Related
- [SMOTE](smote.md)
- [Classification metrics](../ml/supervised/classification-metrics.md)
- [ROC-AUC](../ml/supervised/roc-auc.md)
- [Feature engineering steps](feature-engineering-steps.md)
