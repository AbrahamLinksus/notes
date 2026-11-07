# Multi-query and RAG-Fusion

> Ambiguous user queries retrieve the wrong documents, so query translation has an LLM rewrite the question several ways. Multi-query merges the results, and RAG-Fusion ranks them with RRF.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 74–76)

## Key ideas
- **Query translation**: take the query you received and change or optimise it so the retriever does a better job.
- **Problem:** users often send highly ambiguous queries. The retriever fetches the wrong documents, and that often leads to hallucination.
- **Multi-query** (rewrite approach):
  - Use an LLM to generate several reworded versions of the same question.
  - Embed each one separately and retrieve results for each.
  - Merge everything into one final candidate pool.
  - The retrievals can be vectorised (batched), but it's still expensive, because it needs an extra LLM call to generate the queries.
- **RAG-Fusion** (rewrite approach):
  - Same idea of multiple generated queries, but a **ranking mechanism** is applied across their result lists.
  - **RRF** can be used to fuse them by rank.

## Example
```
user:  "how do I fix memory stuff in my app?"

LLM rewrites:
  q1 "how to find memory leaks in a Python application"
  q2 "reduce memory usage of a long-running service"
  q3 "profiling heap allocations"

multi-query: retrieve(q1) ∪ retrieve(q2) ∪ retrieve(q3) → one pool
RAG-Fusion:  rank lists from q1, q2, q3 → RRF by position → fused top-k
```

## Pitfalls
- Each rewrite costs an LLM call plus a retrieval. Don't generate more variations than you need.
- Plain merging without ranking lets one weak rewrite flood the pool. That's the gap RAG-Fusion's RRF fills.
- Rewrites can drift away from what the user meant. Keep the original query in the set.

## Related
- [Hybrid search and RRF](../retrieval/hybrid-search-rrf.md)
- [Decomposition vs IR-CoT](decomposition-vs-ircot.md)
- [Step-back and HyDE](step-back-and-hyde.md)
