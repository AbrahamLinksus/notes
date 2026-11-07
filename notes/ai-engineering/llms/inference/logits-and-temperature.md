# Logits and temperature

> Temperature divides the logits before softmax: below 1 the distribution sharpens, above 1 it flattens, and at 0 it becomes greedy decoding.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 17–18)

## Key ideas
- **Logit**: the raw, unscaled output score for each token, before any activation is applied.
- Softmax with temperature turns logits into a probability distribution:
  `p(tokenᵢ) = exp(logitᵢ / T) / Σⱼ exp(logitⱼ / T)`
  The numerator is the score for the token in focus. The denominator sums over every token in the vocabulary.
- **Temperature (T)** is a scaling factor that controls how creative, random or predictable the choice is.
  - **T < 1**: the scaled logits get larger, softmax exaggerates the gaps, and the distribution becomes sharp and peaked.
  - **T = 1**: the distribution is unmodified.
  - **T > 1**: the logits shrink towards each other, giving a flat distribution. Around T = 2 the output is varied and random.
  - **T = 0**: greedy decoding. Always pick the single highest-probability token.
- **Is T = 0 always deterministic?** No. Real-world GPU inference adds non-determinism, because the order of floating-point operations can change the result.

## Example
```
logits = [2.0, 1.0, 0.0]

T = 1.0  → probs ≈ [0.67, 0.24, 0.09]
T = 0.5  → logits/T = [4, 2, 0]     → probs ≈ [0.87, 0.12, 0.02]  (sharper)
T = 2.0  → logits/T = [1, 0.5, 0]   → probs ≈ [0.51, 0.31, 0.19]  (flatter)
```

## Pitfalls
- Promising reproducible output just because T = 0. GPU floating-point ordering can still change it.
- Raising temperature to "make it smarter". It only adds randomness, which also raises the hallucination risk.
- Mixing up logits and probabilities. Logits aren't bounded and don't sum to 1.

## Related
- [Decoding strategies](decoding-strategies.md)
- [Hallucination](hallucination.md)
