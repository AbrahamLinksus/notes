# HNSW and IVF indexing

> Indexing organises the embedded chunks into a structure that makes similarity search fast. HNSW does it with a layered graph, and IVF does it with buckets of clusters it can skip.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 83, 85–86)

## Key ideas
- **Indexing** in a RAG system is the step where the embedded chunks are organised into a data structure that supports fast similarity search.
- Example methods: **HNSW** and **IVF**.
- **HNSW (Hierarchical Navigable Small World)**: a graph-based vector search method that arranges the data points in a multi-layered network.
- **IVF (Inverted File)**: groups the data into buckets and skips the irrelevant clusters at search time.
- Compare the brute-force store from my build: it scores the query against *every* vector. An index exists so you don't have to touch every vector.

## Example
```
brute force (my NumPy store):
  query → score all N vectors → top-k

IVF:
  vectors grouped into buckets  [b1] [b2] [b3] [b4]
  query → nearest bucket(s) b2 → score only vectors in b2 → top-k
          (b1, b3, b4 skipped)

HNSW:
  layer 2:  •───────────•            (few nodes, long hops)
  layer 1:  •───•───•───•            (more nodes)
  layer 0:  •─•─•─•─•─•─•─•          (all points, short hops)
  search starts at the top and moves down towards the query's neighbourhood
```

## Pitfalls
- Reaching for an index on a tiny corpus. Brute force over a few thousand normalised vectors is already fast.
- Forgetting that IVF skips clusters. If the right chunk sits in a skipped bucket, it won't be found.
- Mixing up this "indexing" (the search structure) with LangChain's "indexing" (load, split, embed).

## Related
- [Top-k similarity search](top-k-similarity-search.md)
- [Vector database types](vector-database-types.md)
- [RAPTOR and ColBERT](../advanced/raptor-and-colbert.md)
- [LangChain ecosystem](../../langchain/langchain-ecosystem.md)
