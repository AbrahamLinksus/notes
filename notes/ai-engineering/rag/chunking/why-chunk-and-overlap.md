# Why chunk, and overlap

> Whole documents can't be embedded well, because embedding models have input limits and long inputs blur into an averaged vector. Chunks trade retrieval precision against context, and overlap protects sentences that get cut at a boundary.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 33–35)

## Key ideas
- **Why not embed the whole document?**
  1. **Context window limit**: an embedding model has a maximum input length it was trained on. Feed it more and it truncates, or gives out-of-context output.
  2. **Quality degrades with length**: as more tokens blend together, the vector gets diluted and everything averages out. It no longer matches the query vector well.
- **Precision vs richness**:
  - **Smaller units**: each embedding is a sharp, narrow idea. Easy to match, high retrieval precision, but little surrounding context.
  - **Larger units**: more context to work with, but retrieval gets harder and the embedding blurs (the pooling problem).
- **When a boundary lands mid-sentence:**
  1. The embedding loses quality and represents a broken thought.
  2. Even if it's retrieved, the generator doesn't have the grounded fact it needs, so it fills the gap with plausible assumptions, i.e. hallucination.
- **Overlap** duplicates a window of text across neighbouring chunks, so a sentence cut in half still has its context on one side.
- Common practice: overlap by **10–20% of the chunk size**. Above ~25% you get *embedding inflation*: more cost, more compute and more duplication.

## Example
```
"The cause of failure was heat."

no overlap:   [ ...The cause of failure ] [ was heat... ]   → two unrelated embeddings
with overlap: [ ...The cause of failure was heat ] [ failure was heat... ]
chunk_size = 1000, overlap = 200  (20%)
```

## Pitfalls
- Overlap fixes cut sentences but creates duplicates. Handle those again during context assembly.
- Making chunks huge "for context" blurs the embeddings, so precision drops.
- Overlap above 25% mostly adds cost.

## Related
- [Chunking strategies](chunking-strategies.md)
- [Chunk sizing](chunk-sizing.md)
- [LLM embeddings and pooling](../../llms/fundamentals/llm-embeddings-and-pooling.md)
- [Context assembly](../pipeline/context-assembly.md)
