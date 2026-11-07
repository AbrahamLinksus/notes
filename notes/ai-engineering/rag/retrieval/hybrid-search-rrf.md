# Hybrid search and RRF

> Dense search misses exact identifiers and phrasing, so hybrid search adds sparse search too. Reciprocal Rank Fusion merges the two lists by rank, because their raw scores live on incompatible scales.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 51–52)

## Key ideas
- Weaknesses of dense embeddings:
  1. **Exact identifiers**: error codes and IDs are strings with no semantic meaning. Codes 400 and 401 are completely different, but a dense embedding puts them close together.
  2. **Rare words**: there's little learned meaning to go on.
  3. **Exact phrases**: "must exceed 500 ms" ≈ "must not exceed 500 ms" in dense space, even though they mean opposite things.
- Sparse (lexical) search catches exactly these cases, so production systems combine both. That's **hybrid search**.
- **Why not just add the scores?**
  - Dense score: cosine similarity, in (−1, 1).
  - Sparse score: unbounded, in (0, ∞).
  - Combining them naively means one score dominates the other.
- **RRF (Reciprocal Rank Fusion)** uses each chunk's **rank position** in each list instead of its raw score. Ranks don't depend on how each retriever scales its scores, so the two lists become comparable.

## Example
```
query: "error 401 timeout"

dense list:  1. chunk_err400   2. chunk_timeout   3. chunk_err401
sparse list: 1. chunk_err401   2. chunk_timeout   3. chunk_misc

raw scores:  dense 0.83 vs sparse 14.2 → not comparable
by rank:     chunk_timeout is #2 in both, chunk_err401 is #1 sparse / #3 dense
             → fused by position, so neither list's scale dominates
```

## Pitfalls
- Trusting dense search alone for codes, IDs, version numbers or negations.
- Adding or averaging raw dense and sparse scores. The unbounded sparse score swamps the cosine.

## Related
- [Dense vs sparse embeddings](dense-vs-sparse-embeddings.md)
- [Bi- vs cross-encoders](bi-vs-cross-encoders.md)
- [Multi-query and RAG-Fusion](../advanced/multi-query-and-rag-fusion.md)
