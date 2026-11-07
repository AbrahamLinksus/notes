# Decision tree splits: entropy, Gini, information gain

> A decision tree picks, at each node, the feature whose split gives the highest information gain, meaning the biggest drop in impurity.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 17–20)

## Key ideas
- A decision tree is a flowchart-like supervised model. It breaks a problem into a series of simple yes/no questions.
- **Pure split**: every point in the node belongs to one class. **Impure split**: the classes are mixed.
- Two ways to measure impurity:
  - **Entropy**: `H(S) = −p₊ log₂ p₊ − p₋ log₂ p₋`. It's 0 for a pure node and 1 for a 50/50 node.
  - **Gini impurity**: `GI = 1 − Σ pᵢ²`. 0.5 means completely impure (binary). It's cheaper to compute because there's no log, so it's generally preferred.
- **Information gain** decides which feature to split on:
  `Gain(S, f) = H(S) − Σ (|Sᵥ| / |S|) · H(Sᵥ)`
  - Sᵥ = samples in a child, S = total samples. Pick the feature with the **greater** gain.

## Example
Root: 9 Y / 5 N → H(S) = −(9/14)log₂(9/14) − (5/14)log₂(5/14) ≈ 0.94

Split on f₁: C₁ = 6 Y / 2 N (H ≈ 0.81), C₂ = 3 Y / 3 N (H = 1)

```
Gain(S, f₁) = 0.94 − [ (8/14)(0.81) + (6/14)(1) ]
            = 0.94 − 0.892 ≈ 0.048
```
If Gain(S, f₂) = 0.051 > Gain(S, f₁), split on **f₂** first.

## Pitfalls
- The handwritten working gives 0.041 for this example. Recomputing gives ≈ 0.048. The decision doesn't change.
- A tree left to grow fully ends in pure leaves, which means it memorises training data and overfits. This is why random forests exist.
- Gini maxes out at 0.5 (binary) but entropy maxes out at 1, so don't compare their raw values.

## Related
- [Random forest](../ensembles/random-forest.md)
- [AdaBoost](../ensembles/adaboost.md)
- [XGBoost](../ensembles/xgboost.md)
