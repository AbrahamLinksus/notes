# Central limit theorem (CLT)

> As sample size grows, the distribution of sample means approaches a normal distribution, whatever shape the original data has.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (p. 69)

## Key ideas
- Take many samples from a population and compute each sample's mean. Those means form a distribution of their own, the **sampling distribution of the mean**.
- **CLT**: as the **sample size gets larger**, that distribution **approximates a normal distribution**.
- This holds **regardless of how the population is distributed**: skewed, uniform, anything.
- Practical implication: you can treat sample means as normally distributed. That's what lets z-tests, t-tests and confidence intervals work on data that isn't normal.

## Example
Population: die rolls, which are **uniform** (flat), not normal.

```
sample size n = 1   → means look flat:      ▇▇▇▇▇▇
sample size n = 2   → means peak at 3.5:    ▂▅▇▅▂
sample size n = 30  → means are bell-shaped:  ▁▃▇▃▁
                                           centred at 3.5
```
The raw rolls stay flat. Only the **means** become normal.

## Pitfalls
- CLT is about the distribution of **sample means**, not the raw data. The data itself doesn't become normal.
- It needs a "large enough" sample. With tiny samples from very skewed data, the approximation is poor.
- Don't use it as a reason to skip checking the shape of the raw data before something like z-score outlier detection.

## Related
- [Common distributions](common-distributions.md)
- [Sampling methods](../inferential/sampling-methods.md)
- [Confidence intervals, z and t](../inferential/confidence-intervals-z-and-t.md)
