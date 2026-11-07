# Random forest

> A random forest trains many decision trees, each on a bootstrapped sample and a random subset of features, and takes a majority vote so that each tree's overfitting averages out.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 22–24, 65–66)

## Key ideas
- It's a **bagging** algorithm in which every model is a **decision tree**.
- How it's built:
  1. Make a **bootstrapped dataset**: sample rows from the original *with replacement*.
  2. Train a decision tree on it, choosing each split from a **random subset of features**.
  3. Repeat steps 1–2 for many trees.
- Prediction: run the query through **every tree** and take the **majority vote** (or the mean for regression).
- Each tree overfits on its own, but because each is random, the data-specific quirks cancel and the combined output generalises.
- **Out-of-bag (OOB) dataset**: the rows that didn't get into a tree's bootstrap sample. They're useful as a built-in test set.
- **No normalisation needed**: splits are threshold rules, so the scale of a feature doesn't matter. (KNN, by contrast, needs it.)
- **Not impacted by outliers** much.

## Example
```
original rows: 1 2 3 4 5

tree A bootstrap: 1 1 3 4 5   OOB: 2
tree B bootstrap: 2 3 3 4 5   OOB: 1
tree C bootstrap: 1 2 2 4 5   OOB: 3

query → A: yes, B: no, C: yes  → prediction: yes (2 of 3)
```

## Pitfalls
- Bootstrapping samples *with* replacement, so duplicates are expected. That's where the randomness comes from.
- There are two layers of randomness, rows and features. Forget the feature subset and the trees end up correlated.
- One deep decision tree memorises the training data. The forest's whole point is to stop that.

## Related
- [Bagging vs boosting](bagging-vs-boosting.md)
- [Random forest: missing data](random-forest-missing-data.md)
- [Decision tree splits](../supervised/decision-tree-splits.md)
- [K-nearest neighbours](../supervised/k-nearest-neighbours.md)
