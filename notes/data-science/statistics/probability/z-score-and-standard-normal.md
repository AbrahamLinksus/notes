# Z-score and the standard normal distribution

> A z-score gives how many standard deviations a point lies from the mean, and z-scoring normal data produces the standard normal distribution, with μ = 0 and σ = 1.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 56–57)

## Key ideas
- **Z-score**: how many SDs a specific data point is from the mean.
  `z = (xᵢ − μ) / σ`
- Apply it to every point of a normal distribution and you get the **standard normal distribution** (also called the **Z distribution**), with **μ = 0, σ = 1**.
- Uses:
  - Comparing values on different scales.
  - Flagging outliers (|z| > 3).
  - Looking up probabilities in a z-table.
- Related scaling terms:
  - **Standardisation** = z-scoring. Centres the data on mean 0 with SD 1.
  - **Normalisation** rescales the data into the 0–1 range.

## Example
Data: {1, 2, 3, 4, 5, 6, 7} → μ = 4, σ = 2 (population SD)

```
x:  1     2    3     4   5    6    7
z: −1.5  −1  −0.5    0  0.5   1   1.5
```
The new set has mean 0 and SD 1.

Comparing scores across tests: 80 on a test with μ = 70, σ = 5 gives z = 2. 85 on a test with μ = 80, σ = 10 gives z = 0.5. The 80 is the stronger result.

## Pitfalls
- My handwritten example maps this set to {−3 … 3}. That only subtracts the mean. Dividing by σ = 2 gives the values above.
- Z-scoring changes the scale, not the shape. Skewed data stays skewed and doesn't become normal.
- Don't mix up standardisation (mean 0, SD 1) with normalisation (0 to 1).

## Related
- [Common distributions](common-distributions.md)
- [Percentiles and outliers](../descriptive/percentiles-and-outliers.md)
- [Confidence intervals, z and t](../inferential/confidence-intervals-z-and-t.md)
- [Feature engineering steps](../../feature-engineering/feature-engineering-steps.md)
