# AI vs ML vs DL vs DS

> DL sits inside ML, which sits inside AI, and data science draws on all of them along with statistics.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (p. 1)

## Key ideas
- **AI**: an application that can do its task without a human stepping in. A recommendation system is the standard example.
- **ML**: uses statistics to analyse data and learn patterns from it. It's a subset of AI.
- **DL**: a subset of ML that tries to mimic how the human brain works (neural networks).
- **DS**: the overlap of everything. It uses AI, ML, DL and stats together to get answers out of data.
- ML and DL problems split two ways. **Supervised** covers regression and classification. **Unsupervised** covers clustering and dimensionality reduction.

## Example
How the terms nest:

```
┌──────────────── AI ─────────────────┐
│   ┌──────────── ML ────────────┐    │
│   │   ┌──────── DL ───────┐    │    │
│   │   │  neural networks  │    │    │
│   │   └───────────────────┘    │    │
│   └────────────────────────────┘    │
└─────────────────────────────────────┘
        DS overlaps all three
```

A recommender is AI because it runs with no human in the loop. Under the hood it's ML, since it learns from user behaviour, and it might use a DL model for embeddings.

## Pitfalls
- DS isn't one more layer in the nesting. It cuts across all three and adds statistics and domain work.
- "AI" doesn't automatically mean DL. Plenty of AI apps use classical ML or rule-based logic.
- The supervised vs unsupervised split is a property of the problem (labelled data or not), not of the AI/ML/DL layer.

## Related
- [Supervised vs unsupervised](supervised-vs-unsupervised.md)
- [Recommender system types](../../recommender-systems/recommender-system-types.md)
