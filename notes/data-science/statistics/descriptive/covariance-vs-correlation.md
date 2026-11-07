# Covariance vs correlation

> Covariance tells you only the direction two variables move together, while correlation scales it to the range −1 to +1 so you also get the strength.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 50–51)

## Key ideas
- **Covariance**: the relationship between two random variables, i.e. how a change in one affects the other.
  - Positive → direct relation. Negative → inverse relation.
  - Ranges from −∞ to +∞, so it **can't tell you magnitude**.
  - `Cov(x, y) = (1/n) Σ (xᵢ − x̄)(yᵢ − ȳ)`
- **Correlation**: how strongly two variables are related or move together.
  - Ranges from **−1 to +1**.
  - Positive: as one gets bigger, so does the other. Negative: as one gets bigger, the other gets smaller.
  - The **magnitude** shows how strong the relationship is.
  - `ρ(x, y) = Cov(x, y) / (√Var(x) · √Var(y))`
- Comparison:
  ```
                 covariance          correlation
  range          −∞ to +∞            −1 to +1
  direction      yes                 yes
  strength       no                  yes
  comparable     no                  yes (unit-free)
  ```

## Example
```
x = [1, 2, 3]     x̄ = 2
y = [2, 4, 6]     ȳ = 4
Cov = (1/3)[(−1)(−2) + 0 + (1)(2)] = 4/3
Var(x) = 2/3, Var(y) = 8/3
ρ = (4/3) / (√(2/3)·√(8/3)) = (4/3)/(4/3) = 1   → perfect positive
```
Measure y in centimetres instead of metres and Cov is multiplied by 100, but ρ is still 1.

## Pitfalls
- A large covariance doesn't mean a strong relationship. It may just be large units.
- Correlation only captures **linear** co-movement.
- Correlation isn't causation.

## Related
- [Central tendency and dispersion](central-tendency-and-dispersion.md)
- [Linear regression](../../ml/supervised/linear-regression.md)
