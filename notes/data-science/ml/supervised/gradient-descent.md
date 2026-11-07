# Gradient descent

> Gradient descent repeatedly steps each parameter against the slope of the cost function, scaled by a learning rate α, until it converges at the minimum.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 9–10)

## Key ideas
- It's an **iterative optimisation algorithm** that finds a function's minimum by moving in the direction of steepest decrease.
- Convergence rule, applied until the values stop changing:
  `θⱼ := θⱼ − α · ∂J(θ₀, θ₁)/∂θⱼ`
- The derivative is the **slope** of J at the current θ, and its sign sets the direction:
  - Negative slope → `θ := θ − α(−ve)` → θ **increases**.
  - Positive slope → `θ := θ − α(+ve)` → θ **decreases**.
- Either way, θ moves toward the bottom of the U-shaped cost curve.
- **α (learning rate)** is the size of each jump toward the global minimum. Keep it small, because a large α overshoots the minimum.

## Example
On the J vs θ₁ curve from the linear regression example (minimum at θ₁ = 1):

```
start θ₁ = 0    slope < 0 → θ₁ moves right → 0.4 → 0.7 → 0.9 → ~1.0
start θ₁ = 2    slope > 0 → θ₁ moves left  → 1.6 → 1.3 → 1.1 → ~1.0
```
The steps shrink as the slope flattens near the minimum.

## Pitfalls
- If α is too large, θ bounces past the minimum and can diverge. If α is too small, convergence takes forever.
- On a **non-convex** cost function, gradient descent can get stuck in a local minimum where the slope is 0. That's why logistic regression uses log loss instead of squared error.
- The minus sign in the update matters. It's what turns "slope is negative" into "move right". Drop it and you climb the curve instead.

## Related
- [Linear regression](linear-regression.md)
- [Logistic regression](logistic-regression.md)
- [Gradient boosting](../ensembles/gradient-boosting.md)
