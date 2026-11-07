# LLM training pipeline

> Pre-training on raw text gives a base model that only continues text, and alignment (SFT, then RLHF or DPO) teaches it to follow instructions and behave.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 14–15)

## Key ideas
- **Pre-training → base model**
  - Trained on massive amounts of unlabeled, raw text.
  - Its only objective is to continue the given text, in whatever style the text is in.
  - It hasn't learned to follow instructions or to reason. Ask it a question and it may return another, similar question.
  - That's the difference between a base model and an instruct model.
- **Alignment (behaviour)**
  - **SFT (Supervised Fine-Tuning)**, also called **instruction tuning**: train the base model on a curated dataset of instruction → ideal response pairs. This teaches behaviour.
  - **RLHF (Reinforcement Learning from Human Feedback)**: a further push towards ideal, human-like responses.
    1. Generate several responses to the same prompt with the SFT model.
    2. A human ranks the responses.
    3. Train a **reward model** on those rankings.
    4. Use the reward model to train the main model, rewarding it based on its responses.
  - **DPO (Direct Preference Optimization)**: an alternative to RLHF that skips the separate reward model. The preference data becomes a loss function that directly updates the model's weights.

## Example
```
raw text ──pre-train──► base model ──SFT──► instruct model ──RLHF / DPO──► aligned model

Prompt: "What is the capital of France?"
base model:     "What is the capital of Germany? What is the capital of..."
aligned model:  "Paris."
```

## Pitfalls
- Expecting a base model to answer questions. It only continues text.
- Mixing up RLHF and DPO: RLHF trains a reward model, DPO doesn't need one.
- SFT teaches behaviour from examples. It isn't the same as the preference-based step that comes after.

## Related
- [LoRA and QLoRA](lora-and-qlora.md)
- [Encoder vs decoder models](../fundamentals/encoder-vs-decoder-models.md)
- [Hallucination](../inference/hallucination.md)
