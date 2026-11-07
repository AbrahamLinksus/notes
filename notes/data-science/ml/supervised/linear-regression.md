# Linear regression

> Linear regression fits the straight line h(x) = θ₀ + θ₁x that minimises the squared error between predicted and actual values.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 3, 7–8, 13)

## Key ideas
- It models the relationship between a dependent target and one or more independent predictors as a **line of best fit**.
- Hypothesis: `h_θ(x) = θ₀ + θ₁x`
  - θ₀ = **intercept**, the value of y when x = 0.
  - θ₁ = **slope/coefficient**, how much y moves for one unit of movement along x.
- The best line is the one that minimises the **cost function** (mean squared error):
  `J(θ₀, θ₁) = (1/2m) Σ (h_θ(xᵢ) − yᵢ)²`
  - The ½ is only there to make the derivative cleaner.
  - Squaring stops negative and positive errors from cancelling out.
- Assumptions to check: roughly **normal (Gaussian)** features, **standardised** inputs (z-score) for better training, and a **linear** relationship.

## Example
Points (1,1), (2,2), (3,3), m = 3, with θ₀ = 0 so h(x) = θ₁x:

```
θ₁ = 1   → J = (1/6)[(1−1)² + (2−2)² + (3−3)²] = 0
θ₁ = 0.5 → J = (1/6)[0.25 + 1 + 2.25]          ≈ 0.58
θ₁ = 0   → J = (1/6)[1 + 4 + 9]                ≈ 2.3
```
Plotting J against θ₁ gives a U-shaped curve. Its bottom, θ₁ = 1, is the global minimum, which gives the best-fit line.

## Pitfalls
- Outliers pull the line a long way, because squared error punishes big misses heavily.
- On noisy data, J = 0 on training points means overfitting.
- Trying θ values by hand doesn't scale. Use gradient descent.

## Related
- [Gradient descent](gradient-descent.md)
- [R² and adjusted R²](r-squared-and-adjusted-r-squared.md)
- [Ridge and Lasso regression](ridge-and-lasso-regression.md)
- [Z-score and standard normal](../../statistics/probability/z-score-and-standard-normal.md)
