# Supervised vs unsupervised learning

> Supervised learning trains on labelled data to predict a dependent feature, while unsupervised learning has no dependent feature and finds hidden structure on its own.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 1–2, 29)

## Key ideas
- **Supervised ML**: the model learns from a labelled dataset.
  - **Independent features** are the inputs used to make a prediction. There can be any number of them.
  - The **dependent feature** is the value being predicted, usually one per problem.
- Supervised problems come in two kinds:
  - **Regression**: the output is continuous (a price, a temperature).
  - **Classification**: the output is one of a fixed number of classes (spam/not spam).
- **Unsupervised ML** has no dependent feature. The algorithm finds hidden patterns, similarities or structure without human labels or guidance.
  - **Clustering**: groups similar points together (e.g. customer segmentation).
  - **Dimensionality reduction**: shrinks the number of features.

## Example
Same housing data, two framings:

```
features: size, rooms, location   → independent
price                             → dependent

Supervised regression:      predict price (continuous)
Supervised classification:  predict "expensive / cheap" (2 classes)
Unsupervised clustering:    drop price; group similar houses
```

## Pitfalls
- What decides regression vs classification is the **output type**, not the algorithm's name. Logistic *regression* is a classifier.
- An unsupervised result (a cluster ID) has no ground truth, so you can't score it with accuracy the way you score a classifier.
- Don't count the target column among the independent features. That leaks the answer.

## Related
- [AI vs ML vs DL vs DS](ai-vs-ml-vs-dl-vs-ds.md)
- [Linear regression](../supervised/linear-regression.md)
- [Logistic regression](../supervised/logistic-regression.md)
- [K-means and elbow method](../unsupervised/k-means-and-elbow-method.md)
