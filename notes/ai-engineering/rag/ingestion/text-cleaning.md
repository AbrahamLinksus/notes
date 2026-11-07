# Text cleaning

> Clean text has normalised whitespace, no page artifacts, its reading order intact and correct decoding. Garbage in, garbage out.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 26, 28)

## Key ideas
- What "clean" means:
  1. Whitespace is normalised.
  2. It's free of non-content artifacts like page numbers, headers and footers.
  3. The reading order is preserved, so the context survives.
  4. It's properly decoded.
- **Whitespace normalisation**: collapse without destroying structure.
  - Collapse 3+ newlines to 2, so paragraph breaks survive.
  - Collapse repeated spaces and tabs to a single space.
  - Strip trailing whitespace.
- **Boilerplate detection**: a line like "Page 4 of 20" doesn't look like junk on its own. You spot it as a structurally similar line that repeats across pages.
- **Encoding issues**: text that wasn't decoded properly shows up as the replacement character `�` (�).
- Keeping the paragraph breaks matters later, because sentence- and paragraph-aware chunking splits on them.

## Example
```python
import re

def normalize_whitespace(text: str) -> str:
    text = re.sub(r"[ \t]+", " ", text)          # repeated spaces/tabs → one space
    text = re.sub(r" +\n", "\n", text)           # strip trailing whitespace
    text = re.sub(r"\n{3,}", "\n\n", text)       # 3+ newlines → paragraph break
    return text.strip()

normalize_whitespace("Intro.  \n\n\n\nBody\t\ttext ")
# 'Intro.\n\nBody text'
```

## Pitfalls
- Collapsing *all* newlines to spaces destroys the paragraph structure that chunking relies on.
- Trying to remove boilerplate line by line. You have to look for the repetition across pages.
- Ignoring `�` characters. They mean the decoding was wrong further upstream.

## Related
- [Format-specific extraction](format-specific-extraction.md)
- [Deduplication](deduplication.md)
- [Chunking strategies](../chunking/chunking-strategies.md)
