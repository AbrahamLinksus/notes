# P-value, significance and Type I/II errors

> If p ≤ 0.05, reject H₀. A Type I error rejects a true H₀ (a false positive), and a Type II error keeps a false H₀ (a false negative).

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 57–59, 61)

## Key ideas
- **P-value** (between 0 and 1): a statistical measure of how likely it is that your data happened by **random chance** alone.
- **Significance value**: a p-value threshold low enough to show a result didn't happen by pure chance.
- Decision rule (α = 0.05):
  - p ≤ 0.05 → **reject** H₀
  - p > 0.05 → **fail to reject** H₀
- **Type I error**: rejecting H₀ when H₀ is actually **true**. This is a **false positive**.
- **Type II error**: keeping H₀ when H₀ is actually **false**. This is a **false negative**.

## Example
```
                    H₀ true            H₀ false
reject H₀         Type I (FP)          correct ✓
keep H₀            correct ✓         Type II (FN)
```
Drug trial with H₀ = "the drug has no effect":
- p = 0.02 → reject H₀ → conclude it works. If it actually doesn't, that's a **Type I** error.
- p = 0.30 → keep H₀ → conclude no effect. If it actually works, that's a **Type II** error.

## Pitfalls
- A p-value isn't the probability that H₀ is true. It's how surprising the data would be **if** H₀ were true.
- p > 0.05 doesn't prove H₀. You only lack evidence against it.
- Lowering α to cut Type I errors raises the risk of Type II errors.

## Related
- [Hypothesis testing](hypothesis-testing.md)
- [Confidence intervals, z and t](confidence-intervals-z-and-t.md)
- [Classification metrics](../../ml/supervised/classification-metrics.md)
