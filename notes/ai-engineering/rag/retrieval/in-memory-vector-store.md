# In-memory vector store

> Embed chunks in batches, keep the vectors in one contiguous normalised NumPy array with a parallel metadata list, and similarity search becomes a single vectorised operation.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 42–45)

## Key ideas
- **Embedding** turns chunks into vectors: chunk in, vector out.
- For small corpora it's fine to hold every embedding in memory at once. At 100,000+ chunks that gets dangerous, so do it **incrementally**: embed a batch → write it to the store → repeat until done.
- Two ways to store the vectors:
  1. **A field on the chunk**: attach the vector to the Chunk object and pass it around. But search needs all the vectors in **one contiguous 2D array**.
  2. **Parallel arrays**: a 2D vector array plus a metadata list, where `vectors[i]` belongs to `metadata[i]`. This can cause synchronisation bugs if you aren't careful.
- NumPy is fast because it operates on homogeneous, contiguous blocks of numbers (vectorised). Storing each vector together with its metadata would force a slow plain-Python loop.
- **Normalise once, at insertion.** That guarantees every later `search()` can use `a · b = cos θ`.

## Example
```python
import numpy as np

class VectorStore:
    def __init__(self, dim: int = 384):
        self.dim = dim
        self.vectors = np.empty((0, dim), dtype=np.float32)  # n_chunks × dim
        self.metadata: list = []                              # parallel list, same order

    def add(self, chunks):
        vecs = np.array([c.vector for c in chunks], dtype=np.float32)
        vecs /= np.linalg.norm(vecs, axis=1, keepdims=True)   # normalise once
        self.vectors = np.vstack([self.vectors, vecs])
        self.metadata.extend(chunks)
```

## Pitfalls
- Appending to `vectors` and `metadata` in different places so they drift out of sync. Always update both together.
- Embedding a huge corpus in one call and running out of memory. Batch it.
- FastEmbed's `passage_embed` returns a generator. Materialise it with `list()` before using the vectors.

## Related
- [Top-k similarity search](top-k-similarity-search.md)
- [Cosine vs L2 similarity](../../llms/fundamentals/cosine-vs-l2-similarity.md)
- [Vector database types](vector-database-types.md)
