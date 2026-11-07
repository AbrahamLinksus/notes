# Step-back prompting and HyDE

> Step-back retrieves with a more abstract version of the question alongside the original, and HyDE retrieves with a hypothetical answer document instead of the raw query.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 79–81)

## Key ideas
- **Step-back question** (from Google):
  - Ask the LLM for a more abstract, higher-level version of the original query.
  - Retrieve for both. Then feed the abstract question's context and the original question's context into the LLM together to get the answer.
  - Few-shot examples teach the LLM how to step back.
- **HyDE (Hypothetical Document Embeddings)**:
  - Turn the original query into a hypothetical document (an imagined answer), then embed it the same way as the rest of the content.
  - The hope is that this document embeds better than the short, sparse query.
  - Even if the hypothetical document is factually wrong, its genre and structural similarity to a real answer are useful.
  - Idea: a document–document match is closer than a query–document match.

## Example
```
step-back (MuSiQue-style):
  original:  "Jan Šindel was born in what country?"
  step-back: "What is Jan Šindel's personal history?"
  context = retrieve(original) + retrieve(step_back) → LLM

few-shot pair:
  "Could the members of The Police perform lawful arrests?"
  → "What can the members of The Police do?"

HyDE:
  query:      "why does my RAG return irrelevant chunks?"
  hypo doc:   "Irrelevant chunks are usually caused by chunks that are too large..."
  embed(hypo doc) → search      (doc ↔ doc similarity)
```

## Pitfalls
- Using the HyDE document as the answer. It's only a search key, and its facts may be wrong.
- Stepping back too far, so the abstract question retrieves generic context that doesn't help.
- Both techniques add an LLM call before retrieval, which adds latency and cost.

## Related
- [Multi-query and RAG-Fusion](multi-query-and-rag-fusion.md)
- [Decomposition vs IR-CoT](decomposition-vs-ircot.md)
- [Prompt engineering](../../llms/prompting/prompt-engineering.md)
