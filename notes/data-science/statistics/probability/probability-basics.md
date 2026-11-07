# Probability basics and the addition rule

> P(A ∪ B) = P(A) + P(B) − P(A ∩ B), and the overlap term drops out only when A and B are mutually exclusive.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 48–49)

## Key ideas
- **Random experiment**: an experiment you can perform more than once, with an uncertain outcome.
- **Trial**: one performance of a random experiment.
- **Event**: an outcome of a trial. P(E) is its probability.
- **Sample space**: the set of all possible outcomes.
- **Addition rule**:
  - If A and B are **mutually exclusive** (they can't both happen):
    `P(A ∪ B) = P(A) + P(B)`
  - Otherwise:
    `P(A ∪ B) = P(A) + P(B) − P(A ∩ B)`
  - The subtraction removes the overlap, which would otherwise be counted twice.

## Example
One roll of a die. Sample space = {1, 2, 3, 4, 5, 6}.

```
A = roll a 1, B = roll a 2   (mutually exclusive)
P(A ∪ B) = 1/6 + 1/6 = 2/6

A = even {2,4,6}, B = > 3 {4,5,6}   (overlap {4,6})
P(A ∪ B) = 3/6 + 3/6 − 2/6 = 4/6
check: {2,4,5,6} → 4/6 ✓
```

## Pitfalls
- Adding probabilities of events that overlap counts the shared outcomes twice. Subtract P(A ∩ B).
- "Mutually exclusive" isn't the same as "independent". Mutually exclusive events (with non-zero probability) are in fact *dependent*: if one happens, the other can't.
- A sample space has to list every outcome exactly once.

## Related
- [Conditional probability and Bayes](conditional-probability-and-bayes.md)
- [Permutations and combinations](permutations-and-combinations.md)
- [Common distributions](common-distributions.md)
