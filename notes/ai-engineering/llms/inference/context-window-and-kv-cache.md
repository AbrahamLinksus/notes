# Context window and KV cache

> The context window is a hard token limit per forward pass, and the KV cache stops the model recomputing keys and values for tokens it has already processed.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 19–21, 86)

## Key ideas
- **Context window**: the maximum number of tokens (input + output) a model can process in one forward pass. It holds the system prompt, conversation history, retrieved documents and so on.
- It's a **hard cutoff**. Past it, behaviour doesn't gracefully degrade. It's simply undefined.
- When the content won't fit, the options are to **compact** or **truncate** it.
- **KV cache**: caches the key and value vectors. Recomputing them for every already-processed token is redundant, and the cache turns that into a lookup. Its memory use grows linearly.
- **Prefill**: process the input sequence and fill the KV cache. It's parallelisable and compute-bound.
- **Decode**: generate the output, one token at a time.
- **TTFT (time to first token)** is dominated by prefill. **Tokens/sec (throughput)** is dominated by decode.
- **Prompt caching**: the provider reuses the KV cache it already computed for a prompt prefix that hasn't changed, so part of the prefill is skipped.
- **Lost in the middle**: models make the best use of information at the beginning and end of the context.
- **Why long context hasn't replaced RAG:** precision, dynamism, the quadratic attention cost, and compute.

## Example
```
prompt = [system prompt][same docs][new question]
          └──── unchanged prefix ────┘
first call : prefill everything        → slow TTFT
second call: prefix KV reused (cached)  → prefill only [new question]
```

## Pitfalls
- Assuming a model handles overflow gracefully. Plan for compaction or truncation before you hit the limit.
- Putting the key evidence in the middle of a long prompt, where it's most likely to be ignored.
- Changing the start of the prompt on every call, which breaks prompt caching.

## Related
- [Self-attention](../fundamentals/self-attention.md)
- [Context assembly](../../rag/pipeline/context-assembly.md)
- [Decoding strategies](decoding-strategies.md)
