# K-means and the elbow method

> K-means groups unlabelled data around k centroids, alternating between assigning points and moving centroids, and the elbow method picks k where WCSS stops dropping sharply.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 29–30)

## Key ideas
- **Clustering** is unsupervised: it groups unlabelled data.
- In **k-means**, every group has a **centroid** that represents it.
  - k = the number of centroids, which is the number of groups.
  - Points are assigned by **Euclidean distance** to the nearest centroid.
- Steps:
  1. Initialise k centroids.
  2. Assign each point to its nearest centroid.
  3. Move each centroid to the **average** of its assigned points.
  4. Repeat 2–3 until the centroids stop moving.
- **Elbow method** for choosing k:
  - Run k-means for k = 1 … N and record the **WCSS** (within-cluster sum of squares) each time.
  - Plot WCSS against k. Pick the k where the curve drops **abruptly** and then **flattens**: that's the elbow.

## Example
```
WCSS
 │•
 │ •
 │  •
 │   •___
 │       •───•───•───•
 └──────────────────── k
   1  2  3  4  5  6  7
            ↑ elbow at k = 4
```
Going from 4 to 5 clusters barely lowers WCSS, so it isn't worth it.

## Pitfalls
- WCSS always drops as k grows (k = N gives 0). Don't pick the minimum. Pick the elbow.
- It uses Euclidean distance, so scale the features first.
- Where the initial centroids start changes the result. Run it more than once.

## Related
- [Supervised vs unsupervised](../fundamentals/supervised-vs-unsupervised.md)
- [K-nearest neighbours](../supervised/k-nearest-neighbours.md)
