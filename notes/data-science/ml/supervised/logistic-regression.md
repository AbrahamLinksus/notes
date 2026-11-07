# Logistic regression

> Logistic regression is linear regression squashed through a sigmoid into a probability between 0 and 1, trained with log loss so the cost stays convex.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 13–14)

## Key ideas
- It works well for **binary classification**.
- Why not use linear regression for classes?
  - A few outliers can tilt the best-fit line sharply and flip outcomes.
  - The output isn't bounded, so you can't read it as a class probability.
- Fix: put a **sigmoid** activation on the line to squash and bound it.
  - `z = θ₀ + θ₁x`
  - `h_θ(x) = g(z) = 1 / (1 + e^(−z))`, which falls between 0 and 1. A 0.5 threshold splits the classes.
- **Logistic regression = linear regression + a squashing function.**
- Cost function (log loss):
  - `J = −log(h_θ(x))` if y = 1
  - `J = −log(1 − h_θ(x))` if y = 0
- Why not squared error: with the sigmoid inside it, squared error becomes **non-convex**, and gradient descent can stop at a local minimum where the slope is 0. Log loss stays convex.

## Example
```
z = −2 → h = 1/(1+e²)  ≈ 0.12 → class 0
z =  0 → h = 0.5       → boundary
z =  3 → h = 1/(1+e⁻³) ≈ 0.95 → class 1

True y = 1, predict 0.95 → cost = −log(0.95) ≈ 0.05  (small)
True y = 1, predict 0.12 → cost = −log(0.12) ≈ 2.12  (big)
```

## Pitfalls
- It's called "regression" but it's a classifier.
- The 0.5 threshold isn't fixed. Moving it trades precision against recall (see ROC).
- Score it with a confusion matrix, precision and recall, not R².

## Related
- [Linear regression](linear-regression.md)
- [Gradient descent](gradient-descent.md)
- [Classification metrics](classification-metrics.md)
- [ROC–AUC](roc-auc.md)
