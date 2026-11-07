# Chi-square test

> The chi-square test checks claims about population proportions in categorical data by comparing observed counts with expected counts.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 60–61)

## Key ideas
- Use it for claims about **population proportions**.
- It's a **non-parametric** test on **categorical** data (nominal or ordinal).
- Statistic:
  `χ² = Σ (f_o − f_e)² / f_e`
  - f_o = observed frequency
  - f_e = expected frequency
- To decide, look up the critical value (the decision boundary) in a **chi-square table** using the **df** and **α**.
  - χ² > critical value → reject H₀.
  - Equivalently, p ≤ 0.05 → reject H₀.

## Example
A die rolled 60 times. H₀: the die is fair, so f_e = 10 for each face.

```
face   1   2   3   4   5   6
f_o    5  10  15  10   8  12
(f_o−f_e)²/f_e: 2.5  0  2.5  0  0.4  0.4
χ² = 5.8
```
df = 6 − 1 = 5. At α = 0.05 the table gives 11.07. Since 5.8 < 11.07, **fail to reject** H₀: there's no evidence the die is biased.

## Pitfalls
- Use **counts**, not percentages. Percentages give the wrong χ².
- Divide by the **expected** count, not the observed.
- It's for categorical data only. For comparing means of numerical data, use z or t.

## Related
- [Hypothesis testing](hypothesis-testing.md)
- [P-value and Type I/II errors](p-value-and-errors.md)
- [Types of data and statistics](../descriptive/types-of-data-and-statistics.md)
