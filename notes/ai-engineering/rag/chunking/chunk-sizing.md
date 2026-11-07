# Chunk sizing

> Size chunks in tokens, not characters, because embedding models enforce token limits, and choose the size and overlap to match the kind of content.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 39–41)

## Key ideas
- `bge-small-en-v1.5` has a **512-token** limit.
- **Token count matters more than character count**: model context limits are in tokens. Tokens relate to characters, but through frequency, not a fixed ratio.
- Rough approximation: about **0.75 words per token** in English.
- What happens when a chunk is too long:
  - **FastEmbed** silently truncates the excess by default, which causes retrieval misses.
  - Other services (vLLM, Hugging Face text-embeddings) throw a validation error.
- **Trade-offs**:
  - Small chunk → narrow scope, isolated from its context.
  - Large chunk → noisy embedding, with irrelevant text mixed in.
- **Choosing a size by content type:**
  - **Dense technical text** (many related sentences): moderate to large chunks with generous overlap.
  - **Conversational / FAQ** (Q&A pairs): small chunks aligned with natural boundaries. Paragraph-aware splitting with very little overlap, since there's no point bundling unrelated FAQs together.
  - **Code**: logical units, no overlap, structure-aware splitting.
- The general idea is to track where meaningful segments lie and split there.

## Example
```python
from fastembed import TextEmbedding

model = TextEmbedding(model_name="BAAI/bge-small-en-v1.5")

def count_tokens(text: str) -> int:
    tokenizer = model.model.tokenizer          # exact path depends on the FastEmbed version
    return len(tokenizer.encode(text).ids)

assert count_tokens(chunk) <= 512, "would be silently truncated"
```

## Pitfalls
- Setting the chunk size in characters and assuming it fits the model. Measure tokens.
- Trusting FastEmbed not to complain. It truncates silently, and the lost text simply never gets retrieved.
- Using one size for everything. FAQs, dense prose and code need different settings.

## Related
- [Why chunk, and overlap](why-chunk-and-overlap.md)
- [Chunking strategies](chunking-strategies.md)
- [BPE tokenizer](../../llms/fundamentals/bpe-tokenizer.md)
