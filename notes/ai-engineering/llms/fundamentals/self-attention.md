# Self-attention

> Attention lets every token directly look at every other token's representation, whatever the distance, which fixes the long-range dependency problem of RNNs at an O(n²) cost.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 9–11)

## Key ideas
- **Why transformers:** RNNs and LSTMs process tokens one at a time. By token 49 of a 50-token stream, the information from token 1 has been diluted or overwritten. They can't hold context across long ranges.
- Each token produces three vectors from its embedding:
  - **Query (Q)**: "what am I looking for", the current token's request.
  - **Key (K)**: "what do I contain", what the token offers.
  - **Value (V)**: "what do I give if matched", the content that gets passed along.
- It works like a retrieval system:
  1. Compare the current token's query with every other token's key.
  2. Compute each match with a dot product.
  3. Take the relevance-weighted sum of the values.
- This is the same shape as the retrieval step in RAG.
- **Multi-head attention**: a sentence has several kinds of relationships between words, so several attention mechanisms run in parallel, each with its own learned Q, K and V matrices. Their outputs are combined afterwards.
- **Complexity is O(n²)**: n tokens each compare against n tokens.
- **Positional encoding:** self-attention is *permutation invariant*. It works only on content, with no notion of order. Adding a positional embedding injects the "where" signal and restores sensitivity to order.

## Example
```
"A dog bit a man"   vs   "A man bit a dog"
same tokens → identical attention without positions
+ positional embedding → different representations
```

## Pitfalls
- Without positional information, attention can't tell these two sentences apart.
- O(n²) is why long contexts get expensive quickly. Doubling the tokens roughly quadruples the attention work.
- Q, K and V aren't three copies of the embedding. Each comes from its own learned projection.

## Related
- [LLM embeddings and pooling](llm-embeddings-and-pooling.md)
- [Encoder vs decoder models](encoder-vs-decoder-models.md)
- [Context window and KV cache](../inference/context-window-and-kv-cache.md)
