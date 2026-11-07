# Grounding and failure modes

> A grounded prompt tells the model to answer only from labelled sources and to cite them, but RAG can still fail through ignored context, conflicting chunks, empty retrieval or injected instructions.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 55–57)

## Key ideas
- **Grounding prompt**: answer using only the provided context, refuse with a fixed sentence when the context isn't enough, and cite sources as `[Source N]`.
- **Citation resolution**: pull every `[Source N]` out of the answer with a regex, then map N (the result's rank) back to the real chunk metadata (source path, page).
- Use a low temperature (0.1) and return an error result instead of crashing when the LLM call fails.
- **RAG can hallucinate even with correct retrieval when:**
  1. The model ignores the context (an instruction-following failure).
  2. The retrieved texts contradict each other.
  3. Retrieval returns `[]`. The model takes that as "no relevant context exists" and generates from its own weights anyway.
- **Indirect prompt injection**: what if a retrieved chunk contains text telling the model to disregard the user's message? Fix: a prompt template that makes the model treat context as *reference material, not instructions*.
- **Groundedness**: how far the claims are backed by the sources.

## Example
```python
GROUNDING_PROMPT = """Answer using ONLY the provided context below. Do not use outside knowledge.
If the context is not enough, reply exactly: "I don't have enough information in the provided context."
Cite sources like [Source 1].

Context:
{context}

Question: {question}
Answer:"""

def extract_citations(answer: str) -> list[int]:
    return [int(m) for m in re.findall(r"\[Source (\d+)\]", answer)]

groundedness = supported_claims / all_claims     # e.g. 4 / 5 = 0.8
```

## Pitfalls
- Sending an empty context to the LLM. Handle `[]` explicitly and refuse instead.
- Putting retrieved text in the prompt without framing it as references, which lets it be read as instructions.
- Citation numbers that don't line up with the SearchResult ranks. Then the mapping back to sources breaks.

## Related
- [Hallucination](../../llms/inference/hallucination.md)
- [Context assembly](context-assembly.md)
- [RAG evaluation](rag-evaluation.md)
- [Prompt engineering](../../llms/prompting/prompt-engineering.md)
