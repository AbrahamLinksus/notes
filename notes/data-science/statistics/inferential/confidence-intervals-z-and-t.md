# Confidence intervals, z-test and t-test

> A confidence interval is the point estimate ± a margin of error. Use z when the population SD is known and t (with df = n − 1) when it isn't.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 58–60)

## Key ideas
- **Point estimate**: the value of a sample statistic that estimates a population parameter (e.g. sample mean x̄ = 2.9 estimating μ = 3).
- **Confidence interval**: a range of values, worked out from sample data, that's likely to contain the true value of an unknown population parameter.
  `CI = point estimate ± margin of error`
- **Population SD (σ) known → z**:
  `CI = x̄ ± z_(α/2) · σ/√n`
  Test statistic: `z = (x̄ − μ) / (σ/√n)`. Here σ/√n is the **standard error**.
- **Population SD unknown → t** (use the sample SD, s):
  `CI = x̄ ± t_(α/2) · s/√n`, with **degrees of freedom df = n − 1**. Look up t in the table.
  Test statistic: `t = (x̄ − μ) / (s/√n)`
- With n = 1, z reduces to (x − μ)/σ, the ordinary z-score.

## Example
n = 36, x̄ = 2.9, σ = 0.6, 95% confidence (z = 1.96):

```
SE = 0.6 / √36 = 0.1
CI = 2.9 ± 1.96 · 0.1 = 2.9 ± 0.196 → (2.70, 3.10)
```
μ = 3 is inside the interval. If σ were unknown, use s and t with df = 35.

## Pitfalls
- The rule is about whether **σ** is known, not about the sample size alone.
- Divide by √n to get the standard error. Forgetting it makes the interval far too wide.
- 95% confidence describes the *method*: about 95% of intervals built this way contain μ.

## Related
- [Hypothesis testing](hypothesis-testing.md)
- [P-value and Type I/II errors](p-value-and-errors.md)
- [Z-score and standard normal](../probability/z-score-and-standard-normal.md)
- [Central limit theorem](../probability/central-limit-theorem.md)
