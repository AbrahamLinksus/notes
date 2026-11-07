# Chunking strategies

> Fixed-size chunking ignores structure. Recursive character splitting falls back through a hierarchy of separators, and sentence- or paragraph-aware splitting wins when units of meaning matter.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 36–39)

## Key ideas
- **Fixed-size chunking is structure-blind.** It doesn't know what the characters represent:
  - **Code**: even overlap can't fully help.
  - **Tables**: break the column → row dependency.
  - **Headers / Markdown**: break the hierarchy.
- **Recursive character splitting** is the default in many RAG systems.
  - It splits on a hierarchy of separators. If a piece is still too large after the first one, it moves on to the next, and finally falls back to a plain character count.
  - It tends to produce chunks that sit very close to the chunk size every time.
- **Sentence- and paragraph-aware splitting** cuts on semantic boundaries instead. The paragraph breaks kept during whitespace normalisation get used here.
- **A naive sentence split on "." breaks** on decimals, initials and abbreviations. A regex improves it, but it still won't handle every case.
- Sentence-aware splitting beats recursive character splitting **when units of meaning matter**.

## Example
```python
separators = ["\n\n", "\n", " ", ""]
# paragraph not small enough? → split by newline → then by space → then by character

# naive split on "."
"3.9"               → ["3", "9"]
"Dr. Smith arrived" → ["Dr", " Smith arrived"]
"J.R.R. Smith"      → ["J", "R", "R", " Smith"]
```

## Pitfalls
- Using fixed-size chunks for code or tables and losing the structure the content depends on.
- Assuming "." means a sentence ended. Decimals and abbreviations break that.
- Collapsing newlines during cleaning, which leaves recursive and paragraph splitters nothing to work with.

## Related
- [Why chunk, and overlap](why-chunk-and-overlap.md)
- [Chunk sizing](chunk-sizing.md)
- [Text cleaning](../ingestion/text-cleaning.md)
