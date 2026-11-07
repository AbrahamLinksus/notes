# XGBoost

> XGBoost builds trees in sequence on the residuals and picks splits by similarity score and gain, with a λ regulariser in the denominator.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (p. 27)

## Key ideas
- **Extreme gradient boosting**: decision trees built sequentially, each one fixing the errors (**residuals**) left by the one before.
- Steps:
  1. Build a **binary decision tree** using the features.
  2. Compute the **similarity score** of each node from its residuals.
  3. Compute the **information gain** of a split: `gain = C₁ + C₂ − P` (left child + right child − parent similarity).
- Similarity weight:
  - **Classification**: `Σ(residual)² / (Σ p(1 − p) + λ)`, where p is the previous predicted probability.
  - **Regression**: `Σ(residual)² / (number of residuals + λ)`.
- **λ** is a hyperparameter. A bigger λ shrinks the similarity scores, which regularises the trees.
- Keep the split with the highest gain.

## Example
Regression, λ = 0, residuals at the root: [−10, 7, 8]

```
root:   (−10 + 7 + 8)² / 3 = 25/3 ≈ 8.3
split → left [−10]   : 100/1 = 100
        right [7, 8] : 225/2 = 112.5
gain = 100 + 112.5 − 8.3 ≈ 204.2
```
Compare this gain against every other candidate split and keep the largest.

## Pitfalls
- Residuals get **summed before squaring**. Opposite-sign residuals cancel, so a mixed node gets a low score. That's intended.
- The classification and regression denominators are different. Don't use residual count for classification.
- Gain is children minus parent, not parent minus children like entropy-based information gain.

## Related
- [Gradient boosting](gradient-boosting.md)
- [Bagging vs boosting](bagging-vs-boosting.md)
- [Decision tree splits](../supervised/decision-tree-splits.md)
