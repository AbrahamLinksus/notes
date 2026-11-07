# Types of data and types of statistics

> Descriptive statistics summarise the data you have and inferential statistics generalise from a sample to a population, while data itself is either categorical (nominal or ordinal) or numerical (discrete or continuous).

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 44–45)

## Key ideas
- **Statistics**: the branch of maths for studying and analysing data in large quantities.
- **Descriptive statistics** summarise a dataset's characteristics in three basic categories:
  1. Central tendency: mean, median, mode.
  2. Spread/variability: variance, SD.
  3. Frequency distribution: counts.
- **Inferential statistics** draw conclusions about a **population** from a **sample**. They mostly involve estimating parameters and hypothesis testing.
- **Types of data**:
  - **Categorical (qualitative)**: describes data as classes. Grouped, and shown with pie or bar charts.
    - **Nominal**: labels with no order (gender, letters).
    - **Ordinal**: can be ordered, but the gaps don't make mathematical sense (economic status, grade).
  - **Numerical (quantitative)**:
    - **Discrete**: a finite number of possible values. Can't be meaningfully subdivided (count of children).
    - **Continuous**: infinitely many possible values within a range (temperature).

## Example
```
data
├── categorical
│   ├── nominal   → blood group: A, B, O
│   └── ordinal   → grade: A > B > C
└── numerical
    ├── discrete   → number of siblings: 0, 1, 2
    └── continuous → temperature: 36.6 °C
```

## Pitfalls
- Ordinal values can be put in order, but you can't do arithmetic on them. "Grade A − Grade B" means nothing.
- Encoding categories as numbers (1, 2, 3) doesn't make them numerical data.
- Descriptive stats say nothing beyond the data in hand. Generalising takes inference.

## Related
- [Central tendency and dispersion](central-tendency-and-dispersion.md)
- [Sampling methods](../inferential/sampling-methods.md)
- [Hypothesis testing](../inferential/hypothesis-testing.md)
- [Chi-square test](../inferential/chi-square-test.md)
