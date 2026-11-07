# Deduplication

> Deduplicate before embedding, otherwise repeated content counts twice and skews retrieval. A hash catches exact copies, and shingling with MinHash catches near-duplicates.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 30–31)

## Key ideas
- **Why it matters:** if two files with the same content are sent on to embedding, that content becomes twice as strong in the index, which leads to wrong inferences.
- **Exact dedup**: hash the *cleaned* text, e.g. with SHA-256. Cleaning has already removed the noise, so identical content gives an identical hash.
- **Hashing alone isn't enough**: change one character and the hash says "not a duplicate", even though 99% of the document is the same.
- Near-duplicate approaches:
  1. **Embedding similarity**: embed both documents and compute their cosine similarity.
  2. **Shingling / MinHash**: break each document into n-grams (*shingles*) and represent it as the set of its shingles. Compute the **Jaccard similarity** (set overlap) using MinHash to see how many words they share.
- Corpus-level dedup here is a separate job from result-level dedup at retrieval time (MMR, context assembly).

## Example
```python
import hashlib

seen: set[str] = set()
docs = []
for path, cleaned in raw_results:
    h = hashlib.sha256(cleaned.encode("utf-8")).hexdigest()
    if h in seen:
        print(f"SKIPPED (duplicate): {path}")
        continue
    seen.add(h)
    docs.append((path, cleaned, h))
```
Shingles (n = 2) for "the cat sat": {"the cat", "cat sat"}.
Jaccard(A, B) = |A ∩ B| / |A ∪ B|.

## Pitfalls
- Hashing the raw text instead of the cleaned text. Whitespace or header differences then hide real duplicates.
- Relying on exact hashes and missing near-identical versions of the same document.

## Related
- [Text cleaning](text-cleaning.md)
- [Document metadata](document-metadata.md)
- [MMR](../retrieval/mmr.md)
- [Context assembly](../pipeline/context-assembly.md)
