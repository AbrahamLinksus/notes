# Caching basics

> A cache keeps copies of data in fast storage close to whoever asks, so repeat requests skip the slow source. The cost is having to evict and invalidate entries to stay small and correct.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 19–20, 25)

## Key ideas
- **Caching:** store copies of data in a temporary storage location so future requests for that data are served faster.
- It sits **closer to the request source** than the original source, which cuts latency.
- **Hit:** the data was found in the cache. **Miss:** it wasn't, so the request goes to the source.
- **Why not cache everything?** Cache storage is costly and small.
- **Speed order:** L1 > L2 > RAM > disk.
- **Eviction:** removing entries to make space for new ones.
- **Invalidation:** when the DB is updated, cached data goes stale/inconsistent, so the entry has to be deleted or updated.
- **Advantages:**
  - better performance
  - less load on the DB
  - cheaper overall than upgrading the system
- **Disadvantages:**
  - eviction
  - inconsistency
  - complexity
- **When not to cache:**
  1. Cache access time ≈ DB access time.
  2. Access isn't repetitive (high randomness).
  3. There are lots of writes, so the cache keeps falling out of sync.

## Example
```
GET /product/7
  cache.get("product:7") → miss → db.query(...) (50 ms) → cache.set
GET /product/7  (again)
  cache.get("product:7") → hit  (1 ms)

db.update(product 7) → cache entry now stale → invalidate "product:7"
```
Hit ratio decides whether a cache is worth it: 1 hit in 100 lookups just adds a hop.

## Pitfalls
- Mixing up **eviction** (making room) and **invalidation** (staying correct). They solve different problems.
- Caching write-heavy data, where you pay the invalidation cost and rarely get a hit.
- Forgetting the cache is a copy. Stale reads are the default unless you plan invalidation.

## Related
- [Eviction policies](eviction-policies.md)
- [Write strategies](write-strategies.md)
- [Read strategies](read-strategies.md)
- [Cache types](cache-types.md)
