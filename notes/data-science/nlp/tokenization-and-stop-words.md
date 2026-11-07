# Tokenization and stop words

> Tokenization breaks text into tokens, and stop-word removal throws away the common words that carry almost no meaning before any further processing.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 31–32, 34)

## Key ideas
- **NLP**: the branch of AI that helps computers understand, interpret and generate human language.
- Vocabulary:
  - **Token**: a smaller piece of text.
  - **Paragraph**: a distinct section.
  - **Vocabulary**: the unique tokens the model recognises.
  - **Corpus**: a large, structured collection of text data.
- **Tokenization**: breaking large text into tokens. With NLTK:
  - `sent_tokenize(corpus)` → sentences
  - `word_tokenize(corpus)` → words
  - `wordpunct_tokenize(corpus)` → words with the punctuation split off
  - `TreebankWordTokenizer()` → keeps '.' attached to the words, except the final '.', which becomes its own token
- **Stop words**: common words that carry very little meaning for text analysis. NLTK ships a ready-made list you can download, and you can add your own.
- Ideal flow: **remove stop words → stem the words**.

## Example
```python
from nltk.tokenize import sent_tokenize, word_tokenize
from nltk.corpus import stopwords

corpus = "NLP is fun. It is also useful!"
sent_tokenize(corpus)   # ['NLP is fun.', 'It is also useful!']
word_tokenize(corpus)   # ['NLP','is','fun','.','It','is','also','useful','!']

stop = set(stopwords.words("english"))
[w for w in word_tokenize(corpus.lower()) if w.isalpha() and w not in stop]
# ['nlp', 'fun', 'also', 'useful']
```

## Pitfalls
- Different tokenizers handle punctuation differently. Pick one and stick to it for the whole pipeline.
- Lowercase before checking stop words. The NLTK list is lowercase.
- Removing stop words can kill meaning ("not good" → "good"). Edit the list for your task.

## Related
- [Stemming vs lemmatization](stemming-vs-lemmatization.md)
- [One-hot and bag of words](one-hot-and-bag-of-words.md)
- [Subword tokenization (LLMs)](../../ai-engineering/llms/fundamentals/subword-tokenization.md)
