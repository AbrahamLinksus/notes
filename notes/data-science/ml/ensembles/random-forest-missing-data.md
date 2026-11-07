# Random forest: filling missing data

> A random forest fills missing values by starting with a simple guess, then refining it with a proximity matrix that weights similar samples, and repeating until the values stop changing.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 66–67)

## Key ideas
- **Step 1, initial guess**: replace the null values with a measure of central tendency (mean, median or mode).
- **Step 2, build the forest** and run all the data through every tree.
- **Step 3, proximity matrix**: whenever two samples land in the same leaf, add 1 to their entry in the matrix. Samples similar to the one with the missing value build up high proximity.
- **Step 4, normalise**: divide every value in the proximity matrix by the number of trees.
- **Step 5, re-estimate**: use the proximities as weights to recompute the missing value from the similar samples.
- **Repeat** steps 2–5 until the missing values **converge** and stop changing.

## Example
Sample 4 has a missing `weight`. After 10 trees:

```
proximity to sample 4:   s1: 2   s2: 8   s3: 0
÷ 10 trees           →   s1: 0.2 s2: 0.8 s3: 0
weights normalised   →   s1: 0.2 s2: 0.8

weight values:            s1: 60   s2: 80
new guess for s4 = 0.2·60 + 0.8·80 = 76
```
Rebuild the forest with 76 and repeat until the guess settles.

## Pitfalls
- The first mean/median fill is only a starting point, not the final answer.
- Divide the proximities by the **number of trees**. Raw counts grow with forest size.
- It's iterative, so stop at convergence, not after one pass.

## Related
- [Random forest](random-forest.md)
- [Feature engineering steps](../../feature-engineering/feature-engineering-steps.md)
- [Central tendency and dispersion](../../statistics/descriptive/central-tendency-and-dispersion.md)
