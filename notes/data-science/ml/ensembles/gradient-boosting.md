# Gradient boosting (regression)

> Gradient boosting starts from the mean prediction, then keeps adding small trees that predict the remaining residuals, each scaled down by a learning rate.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (p. 68)

## Key ideas
- Steps for regression:
  1. **Initial prediction** = the mean of the target values in the training set.
  2. **Residual** = observed − predicted for every row. Store it in a new column.
  3. Fit a tree that **predicts the residuals**, not the target.
     - Keep the trees small: my notes limit them to 4 leaves, and production systems use 8–32.
     - If several rows fall in the same leaf, the leaf outputs their **mean** residual.
  4. **New prediction** = previous prediction + **learning rate** × tree output.
  5. Recompute residuals (observed − new prediction) and repeat.
- The **learning rate** is there to avoid overfitting. Many small steps beat one big jump.

## Example
Targets: 88, 76, 56 → mean = 73.3

```
round 0:  pred = 73.3   residuals = [14.7, 2.7, −17.3]
tree 1 predicts residuals ≈ [14.7, 2.7, −17.3]
lr = 0.1 → pred = 73.3 + 0.1·[14.7, 2.7, −17.3]
             = [74.8, 73.6, 71.6]
new residuals = [13.2, 2.4, −15.6]   (shrinking)
```

## Pitfalls
- The trees predict **residuals**, not y. Adding a tree's output to the mean is the whole trick.
- Without a learning rate, the first tree fits the residuals exactly and the model overfits.
- In my notes the classification version is only a heading, so this note covers regression only.

## Related
- [Bagging vs boosting](bagging-vs-boosting.md)
- [XGBoost](xgboost.md)
- [AdaBoost](adaboost.md)
- [Gradient descent](../supervised/gradient-descent.md)
