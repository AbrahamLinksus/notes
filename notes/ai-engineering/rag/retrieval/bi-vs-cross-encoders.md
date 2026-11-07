# Bi-encoders vs cross-encoders

> Bi-encoders embed the query and the passage separately, which is cheap and good for searching everything. Cross-encoders read them together with full attention, which is expensive and precise. So retrieve with the first and rerank with the second.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 52–53)

## Key ideas
- **Bi-encoder**: embeds the query and each passage separately, in isolation, then compares the compressed vectors.
  - Cheap. Passage vectors can be computed ahead of time and stored.
- **Cross-encoder**: feeds the query and passage in as one combined input, so the transformer can apply full attention between query tokens and document tokens.
  - More expressive. It catches fine-grained references.
  - Expensive. It has to run once for every query–passage pair.
- **Production shape (two stages):**
  1. **Retrieval**: bi-encoder dense search over the whole corpus returns the top-n candidates.
  2. **Rerank**: a cross-encoder scores that narrow pool, and the result is truncated to k.
- This gets you cross-encoder quality at close to bi-encoder cost, because the expensive model only ever sees n candidates, not the whole corpus.

## Example
```
corpus: 100,000 chunks

stage 1  bi-encoder   query · stored vectors  → top-n = 20   (one matrix product)
stage 2  cross-enc.   score([query, chunk]) × 20             (20 forward passes)
         sort by cross-encoder score → keep k = 5 → generator
```

## Pitfalls
- Running a cross-encoder over the whole corpus. It's far too slow, since nothing can be precomputed.
- Making n too small in stage 1. The reranker can only reorder what retrieval found.
- Expecting bi-encoder scores to capture fine-grained matches. The vector has already compressed those details away.

## Related
- [Hybrid search and RRF](hybrid-search-rrf.md)
- [Top-k similarity search](top-k-similarity-search.md)
- [Self-attention](../../llms/fundamentals/self-attention.md)
- [RAPTOR and ColBERT](../advanced/raptor-and-colbert.md)
