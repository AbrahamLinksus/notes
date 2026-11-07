# Subword tokenization

> Subword tokenization keeps common words whole and breaks rare words into meaningful pieces, which avoids both the huge vocabulary of word-level tokens and the long sequences of character-level ones.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 1–2, 5)

## Key ideas
- **Token**: the atomic unit a model actually operates on. Every input is turned into a sequence of tokens before the model touches it.
- **Token ID**: the integer index of a token in the vocabulary. This number is what actually goes into the model.
- **Sequence length**: the number of tokens in an input. The context window caps it.
- Three ways to split text:
  1. **Word level**: each word is a token. The English vocabulary is too big, anything outside the fixed vocabulary becomes `<unk>`, and run / running / runner are treated as unrelated.
  2. **Character level**: solves the vocabulary problem (only a few hundred characters), but sequences get extremely long. That's expensive because the transformer's cost scales with sequence length, and single characters carry no meaning.
  3. **Subword level**: common words stay single tokens, rare or complex words decompose into fragments.
- Subword wins because it keeps the vocabulary manageable, keeps sequences short, and helps the model generalise across morphology.
- In short: word level fails on vocabulary size, char level fails on sequence length, and subword fixes both by merging frequently used pieces.

## Example
```
"hyperparameterization"
  try:  "hyperparameter" + "ization"
  not found? → "hyper" + "parameter" + "ization"
```
The split stops at meaningful fragments instead of going down to characters, so the semantic knowledge survives.

## Pitfalls
- Word-level tokenization can't handle new words at all. They all collapse into the same `<unk>` token.
- Character level looks like the clean fix, but the sequence-length cost makes it impractical for transformers.
- The model sees token IDs, not words. A token is not the same thing as a word.

## Related
- [BPE tokenizer](bpe-tokenizer.md)
- [LLM embeddings and pooling](llm-embeddings-and-pooling.md)
- [Tokenization and stop words (NLTK)](../../../data-science/nlp/tokenization-and-stop-words.md)
