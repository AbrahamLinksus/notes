# Prompt engineering

> Prompt engineering is structuring, designing and refining the input instructions so the model gives accurate results. A good prompt has a format, a system prompt, context, constraints and an output structure.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 87–89)

## Key ideas
- Components of a proper prompt:
  1. **Input format**: the overall structure of the prompt presented to the LLM.
  2. **System prompt**: sets the overall role, context, purpose and operating guidelines. It gives the foundational parameters that shape everything that follows.
  3. **Context**: the specific details about the query, supplied with the prompt.
  4. **Constraints**: the boundaries and limitations the LLM has to stay within.
  5. **Structured output**: the output format, defined in advance.
- Prompting techniques:
  - **Zero-shot**: just the instruction, no examples.
  - **Few-shot**: include a few worked examples.
  - **Chain of Thought (CoT)**: guide the model through structured intermediate steps.
  - **ReAct (Reason + Act)**: alternate between reasoning and taking actions.
- **Tools and function calling** let an LLM connect with external tools.

## Example
```
SYSTEM:   You are a support assistant for an internal HR knowledge base.   ← role
CONTEXT:  [Source 1] Leave policy... [Source 2] Holiday list...            ← context
RULES:    Answer only from the sources. If unsure, say so.                 ← constraints
FORMAT:   Return JSON: {"answer": str, "citations": [int]}                 ← structured output
QUESTION: How many casual leaves do I get?
```

## Pitfalls
- Leaving out constraints, so the model fills gaps with outside knowledge.
- Asking for structured output without saying exactly what the format is.
- Prompting changes only the input, never the model. If the knowledge isn't there, use RAG.

## Related
- [LoRA and QLoRA](../training/lora-and-qlora.md)
- [Grounding and failure modes](../../rag/pipeline/grounding-and-failure-modes.md)
- [Prompt templates and output parsers](../../langchain/prompt-templates-and-output-parsers.md)
- [Step-back and HyDE](../../rag/advanced/step-back-and-hyde.md)
