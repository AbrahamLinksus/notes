# Hallucination

> A hallucination is fluent, confident output that isn't grounded in any source. That's different from a factual error the model learned from bad training data.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 21–22)

## Key ideas
- **Hallucination**: the model generates content that is fluent and confident but not grounded in any source. It cites non-existent but plausible-sounding data.
- **Factual error vs hallucination**:
  - A **factual error** comes from training. The model saw noisy or contaminated data and learned the wrong thing.
  - A **hallucination** is invented content: plausible, but not backed by anything.
- Causes:
  1. **Sampling randomness**: a high temperature.
  2. **Conflicting content**: the sources disagree.
  3. **Parametric gaps**: the knowledge simply isn't in the weights.
- Two types:
  - **Intrinsic**: the information existed in the source, but the generated output got it wrong.
  - **Extrinsic**: the output adds unverifiable information that wasn't in the source.

## Example
```
Source: "The bridge opened in 1998."

Intrinsic: "The bridge opened in 1989."              (contradicts the source)
Extrinsic: "The bridge opened in 1998 and cost $40M." (adds an unsupported claim)
```

## Pitfalls
- Assuming correct retrieval rules out hallucination. RAG can still hallucinate (see the failure-modes note).
- Blaming every wrong answer on hallucination. If the model learned it from bad data, it's a factual error, and the fix is different.
- Pushing temperature up for creativity on factual tasks makes things worse.

## Related
- [Logits and temperature](logits-and-temperature.md)
- [Grounding and failure modes](../../rag/pipeline/grounding-and-failure-modes.md)
- [RAG evaluation](../../rag/pipeline/rag-evaluation.md)
