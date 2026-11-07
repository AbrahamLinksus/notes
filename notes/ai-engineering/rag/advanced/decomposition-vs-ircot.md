# Decomposition vs IR-CoT

> Decomposition splits a complex question into sub-questions upfront and answers them independently. IR-CoT interleaves retrieval with reasoning, one step at a time, so each step can use what the previous one retrieved.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 77–78)

## Key ideas
- **Decomposition** (sub-question method):
  - Break one complex question into several simpler sub-questions.
  - Retrieve separately for each sub-question, answer each one independently, then combine the answers.
  - All the sub-questions are composed **upfront, at once**, so the retrievals can be vectorised.
- **IR-CoT (Interleaving Retrieval with Chain of Thought)**: an advanced technique for multi-step question answering.
  - Loop: generate a reasoning step → retrieve based on it → generate the next step, informed by what was retrieved → repeat until done.
  - Sub-questions come out one at a time, based on the previous retrieval.
  - Expensive, rules out batch processing, and doesn't scale.
- **Choosing**: ask whether the sub-questions depend on each other.
  - Independent → decomposition (vectorised).
  - Dependent → IR-CoT (not vectorised). A later step needs an earlier step's retrieved answer.

## Example
```
independent: "Compare the leave policy and the travel policy."
  decomposition → s1 "leave policy?"  s2 "travel policy?"   (batch both, combine)

dependent: "Who manages the team that owns service X, and where are they based?"
  IR-CoT → step 1: retrieve "owner of service X"     → team T
           step 2: retrieve "manager of team T"      → person P   (needs step 1)
           step 3: retrieve "location of P"          → answer     (needs step 2)
```

## Pitfalls
- My handwritten decision line has these swapped ("yes → decomposition"). By the definitions above, *dependent* sub-questions need IR-CoT, because decomposition writes every sub-question before any retrieval happens.
- Using IR-CoT for independent sub-questions pays the sequential cost for nothing.

## Related
- [Multi-query and RAG-Fusion](multi-query-and-rag-fusion.md)
- [Step-back and HyDE](step-back-and-hyde.md)
- [Prompt engineering](../../llms/prompting/prompt-engineering.md)
