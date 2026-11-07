# Permutations and combinations

> Use a permutation when order matters (nPr = n!/(n−r)!) and a combination when it doesn't (nCr = n!/(r!(n−r)!)).

studied: 2026-11-07 · status: done · source: Data_Science.pdf (p. 57)

## Key ideas
- **Permutation**: arranging items where **order matters**.
  `nPr = n! / (n − r)!`
- **Combination**: selecting items where **order doesn't matter**.
  `nCr = n! / (r! (n − r)!)`
- The only difference is the extra `r!` in the combination's denominator. It divides out the r! orderings of each chosen group.
- So `nCr = nPr / r!`, which means combinations are never more than permutations.

## Example
Choose 2 of 4 people {A, B, C, D}:

```
President + VP (order matters):
4P2 = 4!/2! = 12
AB BA AC CA AD DA BC CB BD DB CD DC

A 2-person committee (order doesn't matter):
4C2 = 4!/(2!·2!) = 6
AB AC AD BC BD CD
```
Each committee shows up twice in the permutation list (AB and BA): 12 / 2! = 6.

## Pitfalls
- Ask yourself whether swapping two picks gives a different outcome. If yes, it's a permutation. If no, a combination.
- A lock "combination" is really a permutation, because order matters.
- 0! = 1, so nP0 = nC0 = 1 and nCn = 1.

## Related
- [Probability basics](probability-basics.md)
- [Conditional probability and Bayes](conditional-probability-and-bayes.md)
