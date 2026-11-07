# TF-IDF

> TF-IDF scores a word by how often it appears in a sentence, weighted down by how many sentences contain it, so words found everywhere score zero.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 37–39)

## Key ideas
- **Term Frequency–Inverse Document Frequency**: a statistical measure of how important a word is to a document within a corpus.
- `TF = (times the word appears in the sentence) / (number of words in the sentence)`
- `IDF = logₑ(number of sentences / number of sentences containing the word)`
- `TF-IDF = TF × IDF`
- It **ignores words that appear in every sentence**, because their IDF is log(1) = 0. That's how it captures word importance.
- Upsides: fixed vocabulary size, word importance captured.
- Downsides: still sparse, and out-of-vocabulary words are still a problem.

## Example
S1 "good boy", S2 "good girl", S3 "boy girl good"

```
TF          S1    S2    S3        IDF
good        1/2   1/2   1/3       ln(3/3) = 0
boy         1/2   0     1/3       ln(3/2)
girl        0     1/2   1/3       ln(3/2)

TF-IDF      good   boy              girl
S1          0      ½·ln(3/2)        0
S2          0      0                ½·ln(3/2)
S3          0      ⅓·ln(3/2)        ⅓·ln(3/2)
```
"good" is in every sentence, so it scores 0 everywhere.

## Pitfalls
- TF is per sentence, IDF is across the whole corpus. Don't compute IDF per sentence.
- A word that's in every document gets zero weight, even if it matters to your task.
- Like BoW, TF-IDF ignores word order and meaning.

## Related
- [One-hot and bag of words](one-hot-and-bag-of-words.md)
- [Word embeddings: Word2Vec](word-embeddings-word2vec.md)
