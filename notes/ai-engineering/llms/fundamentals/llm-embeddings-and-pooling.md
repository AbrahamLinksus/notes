# LLM embeddings and pooling

> A token starts as a row in the embedding matrix, gains context as it passes through the transformer layers, and pooling collapses the per-token states into one sentence embedding.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 6–9)

## Key ideas
- The **embedding matrix** is a lookup table with one row per vocabulary entry. With a 50,000-token vocabulary and 768-dimensional rows, it's a 50,000 × 768 matrix. Each row is that token's embedding.
- Four kinds of embedding:
  - **Token embedding**: the raw row from the matrix. It has no idea where the token sits.
  - **Positional embedding**: a separate vector that encodes position. It's added to the token embedding before the first transformer layer.
  - **Final hidden state**: the vector for a token after it has gone through the attention layers. It has absorbed context.
  - **Sentence embedding**: a single vector for a whole piece of text, pooled from many token-level hidden states.
- **Pooling** collapses a set of per-token hidden vectors into one fixed-length vector for the sentence:
  1. **Mean pooling**: average all the token hidden states.
  2. **CLS-token pooling**: use the hidden state of the special CLS token.
  3. **Max pooling**.
- **Higher dimensions**: more representation capacity, but more storage per vector and more compute per comparison. Past a point the returns diminish because the extra dimensions capture noise.

## Example
```
token embedding ─┐
                 ├─► transformer layers ─► final hidden states ─► pooling ─► sentence embedding
positional emb. ─┘
```

## Pitfalls
- A token embedding on its own carries no position or context. Only the final hidden state does.
- Bigger embedding dimensions aren't automatically better. Storage and compute grow, and the gains flatten out.
- Different pooling choices give different sentence vectors. Stay consistent across indexing and querying.

## Related
- [Self-attention](self-attention.md)
- [Cosine vs L2 similarity](cosine-vs-l2-similarity.md)
- [Encoder vs decoder models](encoder-vs-decoder-models.md)
- [Dense vs sparse embeddings](../../rag/retrieval/dense-vs-sparse-embeddings.md)
