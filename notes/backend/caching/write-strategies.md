# Cache write strategies

> On a write, choose where the data goes first. Write-through updates cache then DB (consistent, slower writes), write-around skips the cache (more read misses), and write-back updates the DB later and async (fast, risks losing data).

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 21–23)

## Key ideas
- **Goal of invalidation policies:** keep the DB in sync with the cache.
- **1. Write-through:** server → cache → DB. Changes go to the cache first, then to the DB, which keeps them consistent.
  - Cons: you write in 2 places.
  - Cons: entries are cached eagerly, even ones that may never be read.
  - Cons: the synchronous double write means higher latency.
- **2. Write-around:** server → DB directly, and the cache is bypassed.
  - Cons: higher read latency, because recently written data causes cache misses.
- The choice between write-through and write-around hinges on **whether the written data will be read soon**.
- **3. Write-back:** server → cache, and the cache flushes to the DB **asynchronously**.
  - Pros: lower write latency and fewer cache misses.
  - Cons: if power fails before the cache → DB update goes through, the cache empties and the **changes never reach the DB**. Durability is the issue.

## Example
```
write-through:  server ──► cache ──► db       (both, sync)
write-around:   server ──────────► db         (cache untouched)
write-back:     server ──► cache ~~async~~► db

Profile update, read right after   → write-through (next read is a hit)
Log/audit rows, rarely re-read     → write-around (don't pollute cache)
High-rate counters (likes, views)  → write-back (losing a few is OK)
```

## Pitfalls
- Write-back for money or orders: one crash loses committed writes.
- Write-through doesn't remove misses for data that was never written through, like cold reads.
- Write-around plus read-heavy recent data leads to a storm of misses right after every write.

## Related
- [Caching basics](caching-basics.md)
- [Read strategies](read-strategies.md)
- [Eviction policies](eviction-policies.md)
