# Top-k similarity search

> One matrix–vector product scores the query against every stored chunk, and `argpartition` finds the top k without sorting all n scores.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 46–47)

## Key ideas
- Multiplying the stored-vector matrix by the query vector gives one score per chunk.
- Both sides are normalised, so each product is a meaningful similarity number (the cosine).
- The scores have to come back sorted from most to least similar. `k` is how many to return.
- Sorting everything costs O(n log n). Instead, **partition** to pull out the top-k candidates, then sort only those k.
- The result is a list of `(chunk, score)` tuples.
- Edge cases: an empty store returns `[]`, and k is capped at the number of chunks.

## Example
```python
def search(self, query_vector: np.ndarray, k: int = 5) -> list[tuple[Chunk, float]]:
    n_chunks = len(self.metadata)
    if n_chunks == 0:
        return []                                   # empty store, nothing to search
    k = min(k, n_chunks)                            # can't return more than exist

    query_vector = query_vector / np.linalg.norm(query_vector)
    scores = self.vectors @ query_vector            # ① one score per chunk

    top_k_idx = np.argpartition(scores, -k)[-k:]     # ② top-k, unordered
    order = np.argsort(-scores[top_k_idx])          # ③ sort only those k
    final = top_k_idx[order]
    return [(self.metadata[i], float(scores[i])) for i in final]
```
```
scores = [0.12, 0.81, 0.40, 0.77, 0.05], k = 2
argpartition → indices {1, 3}  → sorted → [(chunk1, 0.81), (chunk3, 0.77)]
```

## Pitfalls
- `argpartition` doesn't order the k results. You still have to sort them.
- Forgetting to normalise the query vector, which makes the scores no longer cosines.
- Asking for k larger than the store size without capping it.

## Related
- [In-memory vector store](in-memory-vector-store.md)
- [Retriever design](retriever-design.md)
- [HNSW and IVF](hnsw-and-ivf.md)
