# ROC–AUC

> The ROC curve plots TPR against FPR across every threshold, and the area under it (AUC) lets you compare classifiers with a single number.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (p. 65)

## Key ideas
- **ROC (Receiver Operating Characteristic)** summarises the many confusion matrices you get from different classification thresholds in one plot.
- Axes:
  - y: **TPR** (true positive rate, which is recall) = TP / (TP + FN)
  - x: **FPR** (false positive rate) = FP / (FP + TN)
- Every threshold gives one (FPR, TPR) point. Connecting them draws the curve.
- **AUC (area under the curve)**: use it to compare two ROC curves. The model with more area separates the classes better.

## Example
```
threshold   TPR    FPR
  0.9       0.40   0.05
  0.5       0.75   0.20
  0.1       0.95   0.60

TPR
1.0 |        ____•
    |    __•
    |  •/
    | /
0.0 |/____________ FPR
    0            1.0
```
Model A's curve hugs the top-left and has AUC 0.92. Model B has AUC 0.75. A ranks better.

## Pitfalls
- FPR = FP / (FP + TN), which is *false positive* rate. It isn't the false negative rate, so don't mix them up.
- AUC compares models across all thresholds. It doesn't pick a threshold for you. You still need to choose one point on the curve.
- TPR is just recall under another name. Don't compute it as a separate thing.

## Related
- [Classification metrics](classification-metrics.md)
- [Logistic regression](logistic-regression.md)
