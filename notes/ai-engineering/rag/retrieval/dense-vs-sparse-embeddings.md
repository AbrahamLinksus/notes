# Dense vs sparse embeddings

> Dense embeddings spread meaning across a few hundred uninterpretable dimensions, while sparse embeddings have one slot per vocabulary term. SPLADE learns a sparse vector with term expansion.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 23–24)

## Key ideas
- **Dense embedding**: a fixed-length vector where almost every value is non-zero. Meaning is spread across all the dimensions, and no single dimension is interpretable. E.g. `bge-small` → 384 dimensions.
- **Sparse embedding**: a vector the size of the whole vocabulary, where most values are zero. It's cheaper to store as (index, value) pairs.
- **SPLADE (Sparse Lexical and Expansion Model)**: a sparse retrieval method that combines the structure of sparse embeddings with what dense models learn.
  1. Each token gets a vector the size of the vocabulary (30,522 for BERT).
  2. A BERT-based encoder scores the vocabulary, so related terms ("sit", "sitting") score higher than unrelated words.
  3. All the token vectors are combined by **max pooling** into the final embedding.
- **Term expansion**: raising the scores of tokens similar to the main word inside the fixed vector. That gives a generalised embedding without the dilution dense vectors suffer from.
- **Symmetric models**: both sides of the comparison are the same type of text (sentence vs sentence). No special handling. The question is "are these two similar?"
- **Asymmetric models**: the two sides differ, a short query vs a long passage. The question is "is this passage the answer to the query?" That's why the query and the passages are embedded with different calls.

## Example
```
input: "the cat sat"   (vocab = 30,522 slots)

sparse (SPLADE-style), non-zero entries only:
{ "cat": 2.1, "sat": 1.8, "sit": 1.2, "sitting": 0.9, "kitten": 0.4 }

dense (bge-small): [0.021, -0.113, 0.087, ...]   # 384 values, all non-zero
```

## Pitfalls
- Embedding queries with the passage method on an asymmetric model. Use the query-specific call (`query_embed`).
- Storing sparse vectors as full arrays wastes memory. Store the indices and values.

## Related
- [Hybrid search and RRF](hybrid-search-rrf.md)
- [Bi- vs cross-encoders](bi-vs-cross-encoders.md)
- [LLM embeddings and pooling](../../llms/fundamentals/llm-embeddings-and-pooling.md)
