# Classification metrics

> Precision cares about false positives, recall cares about false negatives, and the F-β score blends the two with β choosing which one matters more.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 6, 15–16)

## Key ideas
- **Confusion matrix** (binary):
  ```
                 actual +   actual −
  predicted +      TP          FP
  predicted −      FN          TN
  ```
- **Accuracy** = (TP + TN) / (TP + FP + FN + TN)
- **Precision** = TP / (TP + FP) = P(actually positive | predicted positive). Of everything I predicted positive, how many really were? Pushes **FP** down.
- **Recall (sensitivity)** = TP / (TP + FN) = P(predicted positive | actually positive). Of all real positives, how many did I catch? Pushes **FN** down.
- **F-β score** = (1 + β²) · (P · R) / (β² · P + R)
  - β = 1 → **F1** = 2PR / (P + R), the harmonic mean. Use it when FP and FN matter equally.
  - β = 0.5 → **F0.5**, when FP is costlier.
  - β = 2 → **F2**, when FN is costlier.

## Example
```
TP = 40, FP = 10, FN = 20, TN = 30
accuracy  = 70/100 = 0.70
precision = 40/50  = 0.80
recall    = 40/60  ≈ 0.67
F1        = 2(0.80·0.67)/(0.80+0.67) ≈ 0.73
```
Spam filter → favour precision (F0.5). Cancer screening → favour recall (F2).

## Pitfalls
- Accuracy is misleading on imbalanced data. With 99% negatives, always predicting "negative" scores 99%.
- Precision and recall pull against each other. Raising the threshold usually lifts precision and drops recall.
- In the F-β formula, β is squared. F2 weights recall 4× in the denominator term, not 2×.

## Related
- [ROC–AUC](roc-auc.md)
- [Logistic regression](logistic-regression.md)
- [P-value and Type I/II errors](../../statistics/inferential/p-value-and-errors.md)
