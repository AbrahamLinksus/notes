# K-nearest neighbours (KNN)

> KNN predicts from the k closest training points: a majority vote for classification, an average for regression.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 16–17, 24)

## Key ideas
- One algorithm that handles both **classification and regression**.
- To predict a new point, measure its distance to every training point and take the **k nearest**.
  - **Classification**: majority category among the k.
  - **Regression**: average of the k neighbours' values.
- Distance metrics:
  - **Euclidean** = √((x₂ − x₁)² + (y₂ − y₁)²), the straight line.
  - **Manhattan** = |x₂ − x₁| + |y₂ − y₁|, the grid path.
- **k is a hyperparameter**. You choose it, the model doesn't learn it.
- **Normalisation is essential**. Distances are scale-sensitive, so a feature in thousands drowns out one in decimals.

## Example
k = 5. Nearest neighbours of the query: 3 red, 2 yellow.

```
classification → red (3 > 2)

regression, neighbour values [10, 12, 11, 15, 12]
→ prediction = 60 / 5 = 12
```
Distance from (1, 2) to (4, 6): Euclidean = √(9 + 16) = 5. Manhattan = 3 + 4 = 7.

## Pitfalls
- It does badly on datasets with **outliers** or **class imbalance**. The majority class keeps winning the vote.
- Unscaled features break it. Normalise first.
- k is yours to tune. A different k can flip the vote (k = 3 might say yellow where k = 5 says red).

## Related
- [Decision tree splits](decision-tree-splits.md)
- [Random forest](../ensembles/random-forest.md)
- [Feature engineering steps](../../feature-engineering/feature-engineering-steps.md)
