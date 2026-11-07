# MMR (Maximal Marginal Relevance)

> MMR picks results one at a time, rewarding relevance to the query and penalising similarity to what's already been picked, so the generator doesn't get the same fact five times.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 50–51)

## Key ideas
- **Problem:** several chunks can say the same thing in different words. They're all valid matches for the retriever, but redundant for the generator.
- **MMR** builds the result list one pick at a time instead of just sorting. Each step takes the candidate with the best combination of:
  1. **Relevance**: similarity between the query and the candidate.
  2. **Redundancy**: similarity between the candidate and the chunks already selected.
- The key move is to **penalise similarity** to what's already been chosen.
- λ controls the balance:
  - λ = 1 → redundancy isn't penalised at all (plain relevance ranking).
  - λ = 0 → redundancy is penalised 100%.
  - **0.5–0.7** balances the two.
- This is dedup *after* ingestion:
  - Ingestion dedup removes corpus-level duplication.
  - MMR removes result-level duplication.

## Example
```
score(c) = λ · sim(query, c) − (1 − λ) · max sim(c, already_selected)

λ = 0.6, candidates: A (rel 0.90), B (rel 0.88, ≈ A: sim 0.95), C (rel 0.70, sim to A 0.20)
pick 1: A
pick 2: B → 0.6·0.88 − 0.4·0.95 = 0.148
        C → 0.6·0.70 − 0.4·0.20 = 0.340  → C wins, B was a near-copy of A
```
Config used: `MMR_LAMBDA = 0.6`, `MMR_CANDIDATE_POOL = 20`. Fetch a bigger pool first, then let MMR pick k from it.

## Pitfalls
- Running MMR over only k candidates leaves it nothing to choose between. Fetch a larger pool.
- Setting λ too low throws away relevant chunks just because they're similar to each other.

## Related
- [Retriever design](retriever-design.md)
- [Deduplication](../ingestion/deduplication.md)
- [Context assembly](../pipeline/context-assembly.md)
