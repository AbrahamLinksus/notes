# Context assembly

> Before generation, the retrieved chunks are reordered against lost-in-the-middle, trimmed to fit the token budget, deduplicated, and formatted with source labels and delimiters.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 53–54)

## Key ideas
- **Ordering**: passing the chunks in plain score order isn't ideal, because of *lost in the middle*. Put the strongest chunks at the edges and the weakest in the middle: `[2, 4, 6, …, 5, 3, 1]`.
- **Token budgeting**: k chunks are available, but the generator also has a fixed context size. Drop the least relevant chunks until it fits.
- **Formatting**: the generator works best with a consistent structure:
  1. **Source labels**, which make citations possible.
  2. **Metadata**, so the model knows where each chunk came from.
  3. **A delimiter** between chunks.
- **De-duplication**: overlap was kept during chunking so sentences wouldn't get cut, but it's redundant here. Options:
  1. Shingling / Jaccard.
  2. Check against the metadata index. This is cheap and preferred.

## Example
```
ranks 1–6 placed as:  [2] [4] [6] [5] [3] [1]
                       ↑ strong        strong ↑
                       weakest in the middle

[Source 1] (handbook.pdf, p. 4)
Employees get 12 casual leaves per year...
---
[Source 2] (policy.docx, section "Leave")
Unused casual leave does not carry forward...
```

## Pitfalls
- My own note: if chunks keep getting truncated, it means k and the max-token limit weren't taken into account while chunking. Go back and fix the chunk size, don't just keep trimming.
- Dropping the source labels means the generator can't cite, and the citations can't be mapped back.
- Leaving overlap duplicates in wastes the budget and repeats the same text to the model.

## Related
- [Context window and KV cache](../../llms/inference/context-window-and-kv-cache.md)
- [Grounding and failure modes](grounding-and-failure-modes.md)
- [MMR](../retrieval/mmr.md)
- [Why chunk, and overlap](../chunking/why-chunk-and-overlap.md)
