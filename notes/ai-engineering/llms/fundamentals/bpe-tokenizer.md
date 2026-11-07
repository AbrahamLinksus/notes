# BPE tokenizer

> Byte Pair Encoding learns its vocabulary by repeatedly merging the most frequent adjacent pair of tokens, which compresses text into shorter token sequences.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 3–6)

## Key ideas
- **BPE (Byte Pair Encoding)** builds its vocabulary from a large text corpus before the model ever sees anything. It's a subword tokenizer and also a data-compression algorithm.
- Training loop:
  1. Start the vocabulary with individual characters as tokens.
  2. Count the frequency of every adjacent token pair.
  3. Merge the most frequent pair into a new token.
  4. Repeat steps 2–3 for a fixed number of merges, a parameter chosen in advance.
- At inference the learned merge rules are re-applied, not re-learned.
- Every merge shortens the sequence, which is the compression part.
- **Letter counting is hard** for an LLM. It only sees token IDs, so the spelling has been abstracted away. It only knows how to spell a word if it memorised the spelling during training.
- **Token cost isn't equal across languages.** BPE vocabularies come from English-dominated corpora, so English gets far more merges. Non-Latin scripts are under-represented, get fewer merges, and use more tokens for the same text.
- APIs charge per token, not per character or word. Rule of thumb: about **1.3 tokens per English word**.

## Example
```
before merge: "t" "h" "e"   → 3 tokens
merge (t,h):  "th" "e"      → 2 tokens
```
After many merges, common words like "the" end up as a single token.

## Pitfalls
- Asking a model to count letters in a word and trusting the answer. It can't see the characters.
- Assuming non-English text costs the same as English. It usually costs more tokens, so more money.
- Thinking the merge rules are learned again at inference. They're fixed after training.

## Related
- [Subword tokenization](subword-tokenization.md)
- [Context window and KV cache](../inference/context-window-and-kv-cache.md)
- [RAG from scratch in LangChain](../../langchain/rag-from-scratch.md)
