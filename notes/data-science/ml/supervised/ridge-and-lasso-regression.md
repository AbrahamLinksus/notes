# Ridge and Lasso regression

> Ridge (L2) and Lasso (L1) add a slope penalty to the cost function to stop overfitting, and Lasso can also drop useless features entirely.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (p. 12)

## Key ideas
- They exist because a line that fits training data perfectly (J = 0) is overfit: low bias on train, high variance on test.
- **Ridge (L2 regularisation)**:
  `cost = Σ(ŷᵢ − yᵢ)² + λ · (slope)²`
  - Penalises big slopes, which flattens the line so it stops chasing every training point.
  - Prevents overfitting and helps balance bias and variance. Gets optimised over iterations.
- **Lasso (L1 regularisation)**:
  `cost = Σ(ŷᵢ − yᵢ)² + λ · |slope|`
  - Works as **feature selection**: it pushes the coefficients of features that don't help accuracy down to zero, so those features get dropped.
  - Prevents overfitting as well.
- **λ** is a hyperparameter that controls how hard to penalise the slope.

## Example
Two training points with a steep fitted line:

```
plain:  J = 0           (fits both points exactly → overfit)
ridge:  J = 0 + λ·θ₁²   (> 0, so a flatter θ₁ now wins)
```
With many features, Lasso might give `θ = [2.1, 0, 0.8, 0]`. Features 2 and 4 are gone.

## Pitfalls
- λ = 0 just gives plain linear regression. A very large λ flattens the line until it underfits.
- Ridge shrinks coefficients but doesn't zero them. If you want feature selection, use Lasso.
- Scale features first. Otherwise the penalty hits large-scale features unfairly.

## Related
- [Bias–variance tradeoff](../fundamentals/bias-variance-tradeoff.md)
- [Linear regression](linear-regression.md)
- [Gradient descent](gradient-descent.md)
