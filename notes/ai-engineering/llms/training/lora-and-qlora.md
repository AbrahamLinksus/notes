# LoRA and QLoRA

> LoRA fine-tunes a model by freezing its weights and training two small low-rank matrices, and QLoRA adds 4-bit quantization of the frozen weights to save even more memory.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 15–16, 22)

## Key ideas
- **LoRA (Low-Rank Adaptation)**
  - Freezes the original base-model weights W.
  - Adds two low-rank matrices, A and B. B is initialised to 0, so training starts from the unchanged model.
  - Only A and B are updated during fine-tuning. W is never touched.
  - At inference the A·B update is combined with the main weights.
- **Quantization** is a memory trick, not fine-tuning. It stores the model's weights at lower numerical precision. Less memory means faster inference, at the cost of some accuracy.
- **QLoRA = LoRA + quantization.** The frozen W is reduced to 4-bit. Some precision is lost, but that's safe: A and B are trained on top, so W only has to stay close enough to its original values.
- **Where fine-tuning fits:**
  - **Prompting** changes nothing about the model, only the input at inference.
  - **RAG** changes the information available by retrieving and injecting it before generation.
  - **Fine-tuning** optimises the model's weights (full, LoRA or QLoRA).

## Example
```
W : d × d   (frozen)
A : d × r   (trainable)
B : r × d   (trainable, starts at 0)        r ≪ d

effective weight = W + A·B

d = 4096, r = 8:
  full update  → 4096 × 4096 ≈ 16.8M params
  LoRA update  → 2 × 4096 × 8 ≈ 65K params
```

## Pitfalls
- Calling quantization a fine-tuning method. It only shrinks storage. QLoRA is the combination with LoRA.
- Initialising both A and B randomly would change the model's output before any training happens. That's why B starts at 0.
- Reaching for fine-tuning when the problem is missing knowledge. That's RAG's job. Fine-tuning changes behaviour.

## Related
- [LLM training pipeline](llm-training-pipeline.md)
- [Prompt engineering](../prompting/prompt-engineering.md)
- [RAG pipeline modules](../../rag/pipeline/rag-pipeline-modules.md)
