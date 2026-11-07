# Recommender system types

> Collaborative filtering recommends what similar users liked, content-based filtering recommends items similar to the ones you already like, and hybrid systems combine the two to cover each one's weak spots.

studied: 2026-11-07 · status: done · source: Data_Science.pdf (pp. 42–43)

## Key ideas
- A **recommender system** uses data and ML to suggest items or content a user is likely to want. It saves the user time.
- Two broad classes:
  - **Personalised**: tailored to the individual user.
  - **Non-personalised**: the same for everyone (e.g. "popular now").
- Three model types:
  1. **Collaborative filtering**: looks at the user's behaviour and finds patterns among people with similar tastes.
     - **Cold start problem**: when there isn't enough data (a new user or item), it can't recommend accurately.
  2. **Content-based filtering**: compares the **content itself**. If two items' vectors are similar, recommend one to people who liked the other.
  3. **Hybrid**: combines both so each covers the other's weakness.
     - Pure collaborative filtering fails on **new items**.
     - Pure content-based can't **surprise** users with anything outside their taste.

## Example
```
You watched: Arrival

Content-based → "MIB"           (its vector is close to Arrival's)
Collaborative → whatever users with tastes like yours watched next
Hybrid        → blend both lists; a brand-new film can still surface
                via its content vector while users still get variety
```

## Pitfalls
- Cold start hits collaborative filtering hardest, because a brand-new item has no ratings.
- Content-based keeps users in a bubble of what they already like.
- "Popular items" lists aren't personalised. Don't count them as a model type.

## Related
- [Word embeddings: Word2Vec](../nlp/word-embeddings-word2vec.md)
- [AI vs ML vs DL vs DS](../ml/fundamentals/ai-vs-ml-vs-dl-vs-ds.md)
