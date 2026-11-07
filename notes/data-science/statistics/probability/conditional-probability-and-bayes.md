# Conditional probability and Bayes' theorem

> Bayes' theorem turns P(B|A) into P(A|B) by weighting it with the prior P(A) and dividing by the marginal P(B).

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 5–6)

## Key ideas
- **Conditional probability** is the chance of A given that B has already happened:
  `P(A|B) = P(A ∩ B) / P(B)`
  It applies to **dependent** events.
- **Bayes' theorem** is used to **invert** a conditional probability:
  `P(A|B) = P(B|A) · P(A) / P(B)`
  - P(A|B) = **posterior** probability
  - P(B|A) = **likelihood**
  - P(A) = **prior** probability
  - P(B) = **marginal** probability
- If A and B are **independent**:
  - `P(A|B) = P(A)` (knowing B tells you nothing about A)
  - `P(A ∩ B) = P(A) × P(B)`

## Example
1% of emails are spam. 90% of spam contains "free". 10% of non-spam contains "free".

```
P(spam) = 0.01                   prior
P(free | spam) = 0.9             likelihood
P(free) = 0.9·0.01 + 0.1·0.99
        = 0.009 + 0.099 = 0.108  marginal

P(spam | free) = 0.9 · 0.01 / 0.108 ≈ 0.083   posterior
```
Even with "free" in it, an email is only about 8% likely to be spam, because spam is rare to start with.

## Pitfalls
- P(A|B) ≠ P(B|A). Confusing them is the classic mistake, and it's exactly what Bayes fixes.
- Ignore the prior and you get wildly overconfident answers (the base-rate fallacy above).
- Only use P(A ∩ B) = P(A)·P(B) after you've confirmed independence.

## Related
- [Probability basics](probability-basics.md)
- [Classification metrics](../../ml/supervised/classification-metrics.md)
