# Multi-representation, RAPTOR and ColBERT

> Advanced indexing changes *what* gets embedded: a keyword-rich summary instead of the raw chunk (multi-representation), a tree of recursive summaries (RAPTOR), or one embedding per token (ColBERT).

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 83–85)

## Key ideas
- **Multi-representation indexing**:
  - Instead of indexing the whole chunk, create a summary that's rich in meaning and full of the chunk's keywords, and embed that.
  - When the summary matches, return the full original document. Summaries go in the vector store, originals in a doc store.
- **RAPTOR (Recursive Abstractive Processing for Tree-Organized Retrieval)**: hierarchical indexing.
  - The question it answers: what if the chunks you need number far more than k?
  - It processes and retrieves data as a tree, combining embeddings, dimensionality reduction and abstractive summaries.
  - Leaves are the raw chunks (the rawest form). Each layer up clusters and summarises the layer below. The root summarises the entire corpus.
- **ColBERT**: a newer paradigm called **late interaction**.
  - The document and the question are each tokenised, and every token gets its own embedding (token-wise embeddings).
  - Matching compares the question's token embeddings against the document's and finds the max for each, instead of comparing one pooled vector per side.

## Example
```
RAPTOR tree
Layer 0 (leaves): [c1] [c2] [c3] [c4] [c5] [c6]
                    └─┬─┘   └─┬─┘   └─┬─┘
Layer 1:          [sum A]  [sum B]  [sum C]      cluster + summarise
                       └─────┼──────┘
Layer 2:                [sum Z]                  root = whole-corpus gist

broad question → matches sum Z / sum B   ·   detail question → matches c4
```

## Pitfalls
- Multi-representation: if the summary drops a key term, the chunk becomes unfindable. Pack it with keywords.
- RAPTOR needs an LLM summarisation pass per cluster per layer, so indexing gets expensive.
- ColBERT stores one vector per token, so storage grows far faster than one vector per chunk.

## Related
- [HNSW and IVF](../retrieval/hnsw-and-ivf.md)
- [Bi- vs cross-encoders](../retrieval/bi-vs-cross-encoders.md)
- [LLM embeddings and pooling](../../llms/fundamentals/llm-embeddings-and-pooling.md)
