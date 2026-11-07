# Decoding strategies

> Greedy always takes the top token, sampling (top-k or top-p) adds controlled randomness, and beam search tracks several candidates. Top-p adapts best, and beam search is a poor fit for chat.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 18–19)

## Key ideas
- **Sampling** is how the next token is chosen while balancing creativity and safety.
- **Top-k**: sample only from the k most likely tokens. Fixed count, variable probability mass.
- **Top-p (nucleus)**: sample from the smallest set of tokens whose cumulative probability reaches p. Fixed probability, variable count.
- **Top-p adapts better**: when the model is confident (one dominant token) the pool shrinks, and when it's uncertain the pool grows. Top-k can cut off reasonable candidates, or be wastefully inclusive.
- **Greedy**: pick the highest-probability next token. Can be globally suboptimal.
- **Beam search**: track several candidate sequences in parallel and pick the one with the highest cumulative probability.
- Beam search isn't used for chat because the safest, most probable path tends to be generic and bland, and it costs a lot of compute.
- **Max tokens**: caps how many tokens the model may generate.
- **Stop sequence**: specific strings that halt generation as soon as they're produced. Useful for setting a boundary.

## Example
```
next-token probs: A 0.50, B 0.30, C 0.15, D 0.05

top-k (k=2)   → {A, B}            always 2 tokens
top-p (p=0.9) → {A, B, C}         0.50+0.30+0.15 = 0.95 ≥ 0.9

confident step: A 0.95, B 0.03 ...
top-p (p=0.9) → {A}               pool shrinks automatically
top-k (k=2)   → {A, B}            still forced to keep 2
```

## Pitfalls
- Treating k as a quality knob. A fixed count can't react to how confident the model is.
- Using beam search for conversation and getting flat, repetitive answers.
- Forgetting max tokens and stop sequences, then getting runaway output or output that spills past the format you wanted.

## Related
- [Logits and temperature](logits-and-temperature.md)
- [Context window and KV cache](context-window-and-kv-cache.md)
