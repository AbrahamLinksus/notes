# Bias–variance tradeoff

> Aim for a model with low bias and low variance: it fits the true pattern and stays stable across different data splits.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 12, 26, 64)

## Key ideas
- **Bias** is the model's inability to capture the true relationship. High bias means it does badly even on the training set.
- **Variance** is how much the fit changes between datasets (different train/test splits). It's a measure of consistency or stability.
- **Overfitting** = low bias, high variance. The model has learnt the *noise* in the training set, so it does well on train data and fails on test data.
- **Underfitting** = high bias. Accuracy is bad on both train and test data.
- Ways to handle overfitting: **regularization** (Ridge/Lasso), **bagging** and **boosting**.
- **Cross-validation**: train the model on several different train/test splits and compare. This exposes variance a single split would hide.

## Example
```
                train acc   test acc   diagnosis
Model A           99%         70%      overfit (low bias, high variance)
Model B           62%         60%      underfit (high bias)
Model C           90%         88%      generalised (low bias, low variance)
```
A regression line that passes exactly through every training point (cost J = 0) is the classic overfit case.

## Pitfalls
- A training cost of zero is a red flag, not a win. It usually means overfitting.
- Checking only one test split can make a high-variance model look fine by luck. Cross-validate.
- Adding model complexity lowers bias but usually raises variance. You're trading one against the other.

## Related
- [Ridge and Lasso regression](../supervised/ridge-and-lasso-regression.md)
- [Bagging vs boosting](../ensembles/bagging-vs-boosting.md)
- [Random forest](../ensembles/random-forest.md)
