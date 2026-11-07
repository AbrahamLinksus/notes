# Support vector machines (SVM)

> An SVM classifies by finding the hyperplane w·x + b = 0 that separates the classes with the widest possible margin.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (p. 28)

## Key ideas
- Supervised algorithm, used **mainly for classification**.
- It finds the **optimal decision boundary**, called a **hyperplane**, separating the classes.
  - In 2D the hyperplane is a line. In 3D it's a plane.
- The hyperplane is `wᵀx + b = 0`.
- Of all the boundaries that separate the data, SVM picks the one that **maximises the margin**, i.e. the distance to the nearest points of each class.
- The points sitting on the margin edges are the **support vectors**. They alone fix where the boundary goes.

## Example
```
   ✗   ✗              ○
     ✗    ┆    │    ┆   ○   ○
   ✗      ┆    │    ┆     ○
          ┆    │    ┆  ○
       margin  │  margin
          wᵀx + b = 0
```
Many lines split ✗ from ○. SVM picks the middle one with the widest gap on both sides, so it should generalise best.

## Pitfalls
- "Best fit" here means maximum margin, not minimum squared error like linear regression.
- Only the support vectors matter. Points far from the boundary don't move it.
- My notes only cover the linear case. Data that isn't linearly separable needs more than a straight hyperplane.

## Related
- [Logistic regression](logistic-regression.md)
- [K-nearest neighbours](k-nearest-neighbours.md)
- [Classification metrics](classification-metrics.md)
