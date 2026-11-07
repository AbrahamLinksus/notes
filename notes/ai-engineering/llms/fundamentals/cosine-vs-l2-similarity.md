# Cosine vs L2 similarity

> For semantic embeddings, meaning lives in the vector's direction, so cosine similarity beats Euclidean distance. Once vectors are normalised, a plain dot product is the cosine.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 7–8)

## Key ideas
- **Cosine similarity** ignores magnitude noise and isolates the directional signal.
- In semantic embeddings, direction is what tends to encode meaning. Two vectors pointing the same way mean similar things, even if their lengths differ.
- **L2 (Euclidean) distance** is the right choice when magnitude matters, like pixel data or sensor data, where the scale carries weight.
- Dot product: `a · b = Σ aᵢ·bᵢ = |a|·|b|·cos θ`.
- If a and b are **unit vectors** (|a| = |b| = 1), then `a · b = cos θ`. The plain dot product is exactly the cosine similarity, with no division needed.
- That's why **normalising embeddings before storing them** is standard practice. You pay the normalisation cost once, and every later comparison is a cheap dot product.

## Example
```python
import numpy as np

a = np.array([3.0, 4.0]);  b = np.array([6.0, 8.0])   # same direction, different length
a_n = a / np.linalg.norm(a)
b_n = b / np.linalg.norm(b)

a_n @ b_n                  # 1.0  → cosine says identical meaning
np.linalg.norm(a - b)      # 5.0  → L2 says they're far apart
```

## Pitfalls
- Using L2 on semantic embeddings punishes vectors that differ only in length.
- Forgetting to normalise and then treating the raw dot product as cosine. It isn't, unless both vectors have length 1.
- Normalising the stored vectors but not the query vector breaks the trick too.

## Related
- [LLM embeddings and pooling](llm-embeddings-and-pooling.md)
- [In-memory vector store](../../rag/retrieval/in-memory-vector-store.md)
- [Top-k similarity search](../../rag/retrieval/top-k-similarity-search.md)
- [Word embeddings and Word2Vec](../../../data-science/nlp/word-embeddings-word2vec.md)
