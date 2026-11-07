# Types of cache

> Where the cache lives sets the trade-off. Distributed caches shard keys across nodes, a global cache is one shared store, a CDN serves static files near users, and server-side vs client-side trades consistency for scale.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 24–26)

## Key ideas
- **Distributed cache:** several cache servers A, B and C hold **no common data** (A ∩ B ∩ C = ∅).
  - Each request is routed to a node by **hash**, e.g. `hash(key) % 3`.
  - **Consistent hashing** is used so that adding or removing a node only rebalances a small share of the keys.
- **Global cache:** all app servers share **one** cache in front of the DB, and the write strategy is implemented there.
- **CDN (Content Delivery Network):** stores static content (HTML, images, etc.) on the CDN for faster access.
- **Server-side caching** (Redis, Memcached): data is cached on the server.
  - Pros: centralized control, consistent data, less redundant processing.
  - Cons: not as scalable, network latency, a single point of failure.
- **Client-side caching:** data is cached on the client's device. HTTP caching is a form of this.
  - Pros: highly scalable, offline access.
  - Cons: data inconsistency, limited storage, security risk.

## Example
```
distributed:  app ─hash(key)%3─► A | B | C     (each key on exactly one node)
global:       app1, app2, app3 ──► one cache ──► db
CDN:          user ──► nearest CDN edge (logo.png, app.js) ──► origin on miss
```
Why consistent hashing: going from 3 to 4 nodes with `% N` moves almost every key, while a hash ring moves only about a quarter.

## Pitfalls
- Plain modulo hashing in a distributed cache means a mass miss storm whenever a node is added or lost.
- A single global or server-side cache is a SPOF. If it goes down, every request falls through to the DB.
- Don't client-cache sensitive or rapidly changing data: you can't invalidate the user's device.

## Related
- [Caching basics](caching-basics.md)
- [Read strategies](read-strategies.md)
- [Session authentication](../auth/session-authentication.md)
- [Indexing and sharding](../databases/indexing-and-sharding.md)
