# Sampling methods

> In probability sampling every member has an equal, random chance of being picked. Non-probability sampling picks by judgement or convenience, which is easier but biased.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (p. 46)

## Key ideas
- **Population**: the entire group you want to draw conclusions about.
- **Sample**: the specific group you actually collect data from. Sample size < population size.
- **Probability sampling** (every member has an equal chance of being selected):
  - **Random**: pick members completely at random.
  - **Systematic**: take every nth member from a list.
  - **Stratified**: divide the population into groups (strata), then pick randomly from **each** group.
  - **Cluster**: randomly select **whole groups** and take everyone in them.
- **Non-probability sampling** (based on judgement or convenience):
  - **Convenience**: whoever is easy for the researcher to reach.
  - **Purposive**: chosen using the researcher's knowledge and expertise.
  - **Voluntary**: members volunteer themselves.

## Example
Survey 100 of a college's 1,000 students across 4 departments:

```
random       → draw 100 IDs from a hat
systematic   → every 10th name on the roll
stratified   → 25 random students from each department
cluster      → pick 2 departments at random, survey all of them
convenience  → whoever's in the canteen at lunch
voluntary    → post a form; whoever fills it in
```

## Pitfalls
- Stratified vs cluster: stratified samples **within** every group, while cluster picks **entire** groups.
- Voluntary samples over-represent people with strong opinions.
- Inference from a non-probability sample doesn't generalise reliably to the population.

## Related
- [Types of data and statistics](../descriptive/types-of-data-and-statistics.md)
- [Central limit theorem](../probability/central-limit-theorem.md)
- [Hypothesis testing](hypothesis-testing.md)
