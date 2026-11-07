# Word embeddings and Word2Vec

> Word embeddings are dense real-valued vectors where words with similar meanings sit close together, and Word2Vec learns them with a small neural network using CBOW or skip-gram.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 39–41)

## Key ideas
- A **word embedding** represents a word as a real-valued vector that encodes its meaning. Words close together in vector space have similar meanings.
- There are two families:
  1. **Count/frequency based**: BoW, TF-IDF.
  2. **Deep learning based**: Word2Vec.
- **Word2Vec**: uses a neural network to learn word associations from a large text corpus.
  - The simplest form is a **2-layer neural network**.
  - The vector values come from how the word relates to the learned feature representation.
  - Two architectures:
    - **CBOW (continuous BoW)**: predict the **target word from its context**. Trains faster on large datasets.
    - **Skip-gram**: predict the **surrounding words from the centre word**. Works better with less data and with rare words.
- **Cosine similarity**: the angle between two word vectors. The score ranges from −1 to 1:
  - 1 → similar
  - 0 → no relation
  - −1 → opposite

## Example
Window size 1 on "the cat sat":

```
CBOW:      [the, sat] → predict "cat"
Skip-gram: "cat"      → predict "the", "sat"

cos(king, queen) ≈ 0.8   (similar)
cos(king, carrot) ≈ 0.0  (unrelated)
```

## Pitfalls
- It's easy to mix up CBOW and skip-gram. **C**BOW = **C**ontext → word. Skip-gram = word → context.
- Cosine similarity measures the angle, not the length. Two vectors pointing the same way score 1 whatever their magnitude.
- Count-based vectors don't capture meaning. Only the learned ones do.

## Related
- [TF-IDF](tf-idf.md)
- [One-hot and bag of words](one-hot-and-bag-of-words.md)
- [Recommender system types](../recommender-systems/recommender-system-types.md)
- [Cosine vs L2 similarity](../../ai-engineering/llms/fundamentals/cosine-vs-l2-similarity.md)
