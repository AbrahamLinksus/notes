# Common distributions: uniform, normal, Bernoulli

> In a normal distribution 68%, 95% and 99.7% of the data falls within 1, 2 and 3 SDs of the mean. Uniform gives every outcome equal odds, and Bernoulli has only the outcomes 0 and 1.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 49, 55–56, 62)

## Key ideas
- A **distribution** is a function or listing of every value a variable can take and how often, or how likely, each one is.
- **Uniform**: every possible outcome is equally likely.
  - **Discrete**: distinct outcomes, each with equal probability (a fair die).
  - **Continuous**: every value in a range is equally likely, including decimals.
- **Gaussian / normal**: a symmetric, bell-shaped, continuous probability curve. Most data clusters around the central average and tapers off equally on both sides.
  - Mean = median = mode.
  - **Empirical rule (68–95–99.7)**:
    - μ ± 1σ → 68%
    - μ ± 2σ → 95%
    - μ ± 3σ → 99.7%
- **Bernoulli**: a single trial whose outcome is either **0 or 1**.

## Example
Heights ~ Normal(μ = 170 cm, σ = 10 cm):

```
            ┌──── 99.7% ────┐
         ┌──── 95% ─────┐
            ┌─ 68% ─┐
  140  150  160  170  180  190  200
            μ−σ   μ   μ+σ
```
About 68% of people are 160–180 cm, and about 95% are 150–190 cm.

Bernoulli: one coin toss with heads = 1, P(1) = 0.5.

## Pitfalls
- The 68–95–99.7 rule only holds for normal data. Don't apply it to skewed distributions.
- Discrete and continuous uniform behave differently: for a continuous one, P(any exact value) = 0.
- My notes only have headings for binomial and log-normal, so they're not covered here.

## Related
- [Z-score and standard normal](z-score-and-standard-normal.md)
- [Central limit theorem](central-limit-theorem.md)
- [Skewness and kurtosis](../descriptive/skewness-and-kurtosis.md)
