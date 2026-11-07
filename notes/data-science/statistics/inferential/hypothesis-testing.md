# Hypothesis testing

> A hypothesis test assumes the null (no effect) and asks whether the experimental data is extreme enough, in one tail or both, to reject it.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 51–53)

## Key ideas
- **Hypothesis testing**: a way to make statistical decisions from experimental data. A hypothesis is an assumption we make about a population parameter.
- **Null hypothesis (H₀)**: the default position that there's **no relationship** between the two measured phenomena. It's written with `=`, `≤` or `≥`.
- **Alternate hypothesis (H₁)**: the observations come from a **real effect** (plus some variation). It's written with `≠`, `<` or `>`.
- **Tailed test**: decides whether to accept or reject H₀ based on where the test statistic falls on a probability distribution curve.
  - **One-tailed**: checks only **one side** of the sampling distribution (H₁ has `<` or `>`).
  - **Two-tailed**: checks **both sides** (H₁ has `≠`).
- How a test runs:
  1. State H₀.
  2. State H₁.
  3. Run the experiment.
  4. Reject or fail to reject H₀.

## Example
Claim: the average delivery time is 30 min.

```
two-tailed:  H₀: μ = 30    H₁: μ ≠ 30   (is it different at all?)
one-tailed:  H₀: μ ≤ 30    H₁: μ > 30   (is it slower?)

         two-tailed                  one-tailed (right)
   reject │      │ reject                 │ reject
   ▁▃▅▇█▇▅▃▁                     ▁▃▅▇█▇▅▃▁
  ↑                ↑                       ↑
```

## Pitfalls
- You "fail to reject" H₀. You never "prove" it.
- The equals sign always goes in H₀, never in H₁.
- Choose one- or two-tailed **before** you see the data, not after.

## Related
- [P-value and Type I/II errors](p-value-and-errors.md)
- [Confidence intervals, z and t](confidence-intervals-z-and-t.md)
- [Chi-square test](chi-square-test.md)
- [Sampling methods](sampling-methods.md)
