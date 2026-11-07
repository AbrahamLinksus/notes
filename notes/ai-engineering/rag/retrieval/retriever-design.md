# Retriever design

> The vector store only returns the raw top-k. The retriever owns the query side: it embeds the query, applies metadata filters and a score threshold, and returns ranked SearchResults.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 48–49)

## Key ideas
- `vector_store.search()` returns the top-k and nothing more. The retriever wraps it.
- The retriever's responsibilities:
  1. **Embed the query text.** The retriever must embed before calling `search()`. Pushing raw query text into the store step would create coupling errors.
  2. **Apply metadata filters**: decide which subset of the corpus is even eligible for this query.
  3. **Apply a score threshold**: top-k always returns k results, even when their scores are too low to be useful. The threshold drops those.
- The output is `SearchResult(chunk, score, rank)`, where `rank` is the 1-indexed position in the final ranked list.
- Use the query-specific embed call. The model is asymmetric, so queries and passages are embedded differently.

## Example
```python
@dataclass
class SearchResult:
    chunk: Chunk
    score: float
    rank: int          # position in the final ranked list, 1-indexed

def retrieve(query, store, k=5, score_threshold=0.3, filters=None):
    if len(store.metadata) == 0:
        return []
    qv = list(model.query_embed(query))[0]           # asymmetric: query_embed
    qv = qv / np.linalg.norm(qv)

    filtered = []
    for chunk, score in store.search(qv, k=k):
        if score < score_threshold:
            continue                                 # didn't clear the bar
        if filters and not _matches_filters(chunk, filters):
            continue
        filtered.append((chunk, score))
    return [SearchResult(c, s, rank=i + 1) for i, (c, s) in enumerate(filtered)]
```

## Pitfalls
- Trusting top-k blindly. With no threshold, irrelevant chunks still reach the generator.
- Filtering *after* top-k can leave fewer than k results. That's expected, not a bug.
- Embedding the query with `passage_embed` on an asymmetric model.

## Related
- [Top-k similarity search](top-k-similarity-search.md)
- [MMR](mmr.md)
- [Routing and query construction](../advanced/routing-and-query-construction.md)
- [Document metadata](../ingestion/document-metadata.md)
