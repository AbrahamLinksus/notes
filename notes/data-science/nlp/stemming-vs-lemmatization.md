# Stemming vs lemmatization

> Stemming chops affixes off to reach a crude root that may not be a real word, while lemmatization maps each word to its dictionary form (the lemma) using its part of speech.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 32–35)

## Key ideas
- **Stemming**: a preprocessing step that reduces words to a root/base form by stripping suffixes and prefixes.
  - Downside: the meaning can change, and the result may not be a real word.
  - NLTK stemmers:
    - `PorterStemmer().stem(word)`: the standard one.
    - `RegexpStemmer`: uses a regex to strip the prefixes and suffixes you give it.
    - `SnowballStemmer`: supports multiple languages, lowercases words, and works better than Porter.
- **Lemmatization**: groups the different forms of a word into one base or dictionary form, the **lemma** (root word).
  - NLTK: `WordNetLemmatizer()`, then `.lemmatize(word, pos=...)`.
  - **POS** argument: noun `'n'`, verb `'v'`, adjective `'a'`, adverb `'r'`.
  - The lemma you get back depends on the `pos` you pass. That's where part-of-speech tagging comes in.

## Example
```python
from nltk.stem import PorterStemmer, WordNetLemmatizer
ps, wl = PorterStemmer(), WordNetLemmatizer()

ps.stem("history")            # 'histori'    ← not a word
ps.stem("congratulations")    # 'congratul'
wl.lemmatize("going", pos="v")  # 'go'
wl.lemmatize("going", pos="n")  # 'going'    ← pos changes output
```

## Pitfalls
- Stems like "histori" aren't words. Don't use stemming where the output has to be readable.
- The lemmatizer defaults to noun, so verbs pass through unchanged unless you set `pos="v"`.
- Stemming is quick and rough, lemmatization is slower and correct. Choose based on whether meaning matters.

## Related
- [Tokenization and stop words](tokenization-and-stop-words.md)
- [One-hot and bag of words](one-hot-and-bag-of-words.md)
