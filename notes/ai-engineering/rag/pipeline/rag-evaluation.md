# RAG evaluation

> Evaluate a RAG system in two halves, retrieval (did the right chunks come back?) and generation (is the answer grounded, relevant and complete?), against a golden Q&A set.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 59–60)

## Key ideas
- **Retrieval metrics:**
  1. **Hit rate**: for a given query, did the retrieved set contain at least one relevant chunk?
  2. **MRR**: listed in my notes as a retrieval metric, without detail.
  3. **Context precision**.
  4. **Context recall**: how much of the information the generator needed actually made it into its context window.
- **Generation metrics:**
  1. **Groundedness / faithfulness**.
  2. **Answer relevance**.
  3. **Completeness**.
- **RAGAS and DeepEval** are open-source evaluation frameworks.
  - RAGAS centres on faithfulness, relevance, context precision and context recall.
  - Both work by using an **LLM as a judge**.
- **Golden Q&A set**: pre-written correct question–answer pairs, drawn from a single source or from combined or synthesised sources. Evaluate against it.

## Example
```
golden set (3 questions), k = 5

Q1: relevant chunk retrieved?  yes
Q2: relevant chunk retrieved?  no
Q3: relevant chunk retrieved?  yes
hit rate = 2 / 3 ≈ 0.67

Q1 answer: 5 claims, 4 supported by context → faithfulness = 0.8
```

## Pitfalls
- Only evaluating the final answer. A bad answer can come from retrieval or from generation, so measure both halves.
- A golden set built only from single-source questions misses the multi-source, synthesised cases.
- LLM-as-a-judge scores are themselves model outputs. Spot-check them.

## Related
- [Grounding and failure modes](grounding-and-failure-modes.md)
- [Hallucination](../../llms/inference/hallucination.md)
- [Retriever design](../retrieval/retriever-design.md)
