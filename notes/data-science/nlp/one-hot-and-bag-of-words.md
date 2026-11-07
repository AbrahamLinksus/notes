# One-hot encoding and bag of words

> One-hot turns each word into a sparse binary vector, and bag of words turns a whole sentence into a vector of word counts. Both ignore word order and meaning.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 35–37)

## Key ideas
- **One-hot encoding**: converts categorical text labels into a numeric binary format the model can process. It's a **sparse** representation.
  - Tools: sklearn `OneHotEncoder`, pandas `pd.get_dummies()`.
  - Downsides: sparse matrix (can cause overfitting), limited vocabulary, wasted memory, fixed input size, and semantic and positional meaning are ignored.
- **Bag of words (BoW)**: converts text into numeric vectors by **counting word frequencies**, ignoring grammar and word order.
  - Steps: lowercase everything → remove stop words → build the vocabulary with word frequencies → order by frequency → make each sentence's vector from the vocabulary.
  - **Binary BoW** marks presence with 1/0. **Frequency BoW** stores the count, so it goes up for repeats.
  - Upsides: simple, and the input size is flexible.
  - Downsides: sparse matrix (memory and overfitting), no semantic or positional meaning.

## Example
Sentences: S1 "good boy", S2 "good girl", S3 "boy girl good"

```
vocab (by freq): good(3) boy(2) girl(2)

        good boy girl
S1  →  [ 1,   1,   0 ]
S2  →  [ 1,   0,   1 ]
S3  →  [ 1,   1,   1 ]

one-hot of "boy" alone → [0, 1, 0]
```

## Pitfalls
- "dog bites man" and "man bites dog" get the **same** BoW vector because order is lost.
- Every word counts equally in BoW, so frequent words that tell you nothing dominate. TF-IDF fixes that.
- Words that weren't in the training vocabulary just disappear at prediction time.

## Related
- [TF-IDF](tf-idf.md)
- [Word embeddings: Word2Vec](word-embeddings-word2vec.md)
- [Tokenization and stop words](tokenization-and-stop-words.md)
