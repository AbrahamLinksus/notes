# AdaBoost

> AdaBoost chains decision stumps, gives each one a vote weighted by how well it did, and boosts the weights of misclassified rows so the next stump concentrates on them.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 24–25, 67)

## Key ideas
- **Adaptive boosting** combines many weak classifiers in sequence into one highly accurate strong classifier.
- **Stump**: a tree with 1 root node and 2 leaves. Each one is a weak learner.
- Votes are **weighted, not uniform**. Every stump depends on the one before it.
- Steps:
  1. Give every row the same sample weight, 1/n.
  2. Fit a stump. **Total error (TE)** = sum of the weights of the rows it got wrong.
  3. **Performance of stump** = ½ · ln((1 − TE) / TE). This becomes the stump's say in the final vote.
  4. Update the weights:
     - correct rows: `w · e^(−performance)` (shrinks)
     - wrong rows: `w · e^(+performance)` (grows)
  5. **Normalise**: new weight / Σ new weights.
  6. The next stump trains on the revised weights.

## Example
7 rows, weight 1/7 each. The stump gets 1 row wrong → TE = 1/7.

```
performance = ½ ln((1 − 1/7)/(1/7)) = ½ ln 6 ≈ 0.895
correct:   (1/7)·e^(−0.895) ≈ 0.05
incorrect: (1/7)·e^(+0.895) ≈ 0.349
sum = 6(0.05) + 0.349 = 0.649
normalised: correct ≈ 0.07, incorrect ≈ 0.537
```
The one wrong row now carries about half the total weight.

## Pitfalls
- Remember to normalise. Without it the weights don't sum to 1.
- Low TE → high performance → a big say in the vote. If TE = 0.5, the stump gets no say at all.
- Correct rows get e^(−perf) and wrong rows get e^(+perf). It's easy to swap the signs.

## Related
- [Bagging vs boosting](bagging-vs-boosting.md)
- [Gradient boosting](gradient-boosting.md)
- [Decision tree splits](../supervised/decision-tree-splits.md)
