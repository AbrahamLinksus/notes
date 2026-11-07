# Bagging vs boosting

> Bagging trains models in parallel on random subsets and votes or averages to cut variance, while boosting trains weak learners in sequence so each one fixes the previous one's errors.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 21–22)

## Key ideas
- **Ensemble techniques** combine several ML models to get predictions that are more accurate and stable than any single model can manage on its own.
- **Bagging (bootstrap aggregating)**:
  - Train several models **independently and in parallel**, each on a random sample of the data.
  - Combine with a **majority vote** (classification) or the **mean** (regression).
  - Goal: **reduce variance**.
  - Example: random forest.
- **Boosting**:
  - Train models **sequentially**. Each new model focuses on the errors or misclassified instances of the one before it.
  - A chain of **weak learners** adds up to one **strong learner**.
  - Examples: AdaBoost, gradient boosting, XGBoost.

## Example
```
BAGGING (parallel)                    BOOSTING (sequential)

data ─┬─ sample → M1 (log. reg.) ─┐   data → M1 → errors → M2 → errors → M3 → …
      ├─ sample → M2 (dec. tree) ─┼─ vote / mean   weak     weak       weak
      ├─ sample → M3 (KNN)       ─┤            └──────────────┬───────────┘
      └─ sample → M4 (dec. tree) ─┘                    strong learner
```
The bagging models can be different algorithms. In a random forest they're all decision trees.

## Pitfalls
- Bagging mainly fixes **variance** (overfitting). Boosting attacks the errors left over by the previous learners.
- Boosting can't run in parallel, because each model needs the one before it.
- The vote is majority for classification and mean for regression. Don't average class labels.

## Related
- [Random forest](random-forest.md)
- [AdaBoost](adaboost.md)
- [Gradient boosting](gradient-boosting.md)
- [XGBoost](xgboost.md)
- [Bias–variance tradeoff](../fundamentals/bias-variance-tradeoff.md)
