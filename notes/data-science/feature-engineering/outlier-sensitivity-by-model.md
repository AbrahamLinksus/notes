# Which models are sensitive to outliers

> Models that rely on probabilities, margins or splits mostly shrug off outliers, while models that fit a line or use means get pulled by them.

studied: 2026-11-25 · status: done · source: Data_Boring.pdf (pp. 5–6)

## Key ideas
- An **outlier** is a data point or record that deviates from the collective records, and it skews the whole data distribution.
- **Not sensitive**:
  - **Naive Bayes**: relies on probability and frequency, not distance or boundary lines.
  - **SVM**: the decision boundary depends mainly on the support vectors closest to the margin, not the whole dataset.
  - **Decision trees**: minimal effect on classification. Some effect in regression because the mean is used.
  - **KNN**: marked as not sensitive in the notes.
- **Sensitive**:
  - **Linear regression**: outliers pull the best-fit line toward extreme values, reducing accuracy.
  - **Logistic regression**: skews boundaries and slows down optimization.
  - **K-means**: marked as sensitive in the notes.

## Example
```
Linear regression on x = 1..8 with one y = 100 outlier
→ the line tilts toward the outlier and fits the other 7 points worse.
SVM: only the points nearest the margin matter, so a far-away point changes nothing.
```

## Pitfalls
- "Insensitive" doesn't mean "ignore outliers". Decision trees in regression still use means, so they're affected.
- Check the model before spending time on outlier removal.

## Related
- [Outlier removal: bounds and IQR](../statistics/descriptive/percentiles-and-outliers.md)
- [Linear regression](../ml/supervised/linear-regression.md)
- [Logistic regression](../ml/supervised/logistic-regression.md)
- [Support vector machines](../ml/supervised/support-vector-machines.md)
- [K-nearest neighbours](../ml/supervised/k-nearest-neighbours.md)
- [K-means](../ml/unsupervised/k-means-and-elbow-method.md)
