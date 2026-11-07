# Encoder vs decoder models

> Encoders see the whole input in both directions and are built to understand. Decoders see only the past and are built to generate, which is why LLMs are decoders.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 12–14)

## Key ideas
- **Encoder-only** (e.g. BERT): built to understand and represent, not to produce text. Each token attends to every token before and after it, which gives rich contextual representations.
- **Decoder-only** (e.g. GPT, Claude): built to predict the next token from everything before it. Each token only sees context up to itself, which suits open-ended generation.
- **Encoder-decoder** (e.g. BART, T5): two stacks. The encoder reads the full input bidirectionally and feeds the result into the decoder, which uses causal attention. Good for fixed tasks like summarisation and translation, where the whole source has to be read first.
- **Bidirectional attention**: no mask, so every token sees every other token (encoder style).
- **Causal attention**: a mask blocks the tokens after the current one.
- **Why masks:** training has to simulate inference. Without the mask, the model would already see the next token, which leaks the answer.
- **BERT is good at embeddings** because every hidden state is informed by the full sentence in both directions, so the pooled sentence embedding is rich. It's bad at generation because it was never trained to predict the next token.
- **Decoders for LLMs**: they scale with more raw data and parameters, because each output token is appended and fed back as input. That handles open-ended generation, reasoning chains and few-shot tasks. Encoder-decoders assume a fixed input-output shape, so they're less flexible.

## Example
```
"The cat sat on the mat", predicting after "sat"
encoder (no mask):   sat → sees The, cat, on, the, mat
decoder (causal):    sat → sees The, cat           (future masked)
```

## Pitfalls
- Using a decoder's hidden states as sentence embeddings. An encoder like BERT gives better embeddings.
- Training without a causal mask quietly teaches the model to copy the next token instead of predicting it.

## Related
- [Self-attention](self-attention.md)
- [LLM embeddings and pooling](llm-embeddings-and-pooling.md)
- [LLM training pipeline](../training/llm-training-pipeline.md)
