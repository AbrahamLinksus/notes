# Cache read strategies

> On a read, decide who talks to the DB. In cache-aside the app does (4 hops), in read-through the cache does (and collapses concurrent misses), and refresh-ahead reloads hot keys before their TTL runs out.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 23–24)

## Key ideas
- **1. Cache-aside:** the **server handles everything**.
  1. The server checks the cache.
  2. On a miss, it queries the DB.
  3. The DB returns the data.
  4. The server writes it to the cache.
  - That's **4 hops** on a miss.
- **2. Read-through:** the server only talks to the cache, and the cache fetches from the DB on a miss.
  - With **concurrent requests**, only **one fetch** goes through to the DB. The rest then get cache hits.
- **3. Refresh-ahead:** for **hot data**.
  - **TTL** (Time To Live) is how long an entry is valid.
  - **RAF** (Refresh-Ahead Factor) sets a threshold of RAF × TTL.
  - An access after that threshold triggers a background refresh, so hot keys never actually expire mid-traffic.

## Example
Refresh-ahead, TTL = 60 s, RAF = 0.5 → threshold = 30 s:
```
t = 0   key added to cache
t = 20  read → 20 < 30 → no-op, serve cached
t = 40  read → 40 > 30 (close to expiry) → serve cached + refresh from DB
```
Cache-aside in code:
```python
def get_user(uid):
    u = cache.get(uid)            # hop 1
    if u is None:
        u = db.fetch(uid)         # hops 2–3
        cache.set(uid, u, ttl=60) # hop 4
    return u
```

## Pitfalls
- With cache-aside, 100 simultaneous misses mean 100 DB queries. Read-through's single fetch avoids that stampede.
- Refresh-ahead on cold keys wastes DB work refreshing data nobody reads again.
- Read strategy and write strategy are separate choices. Pair them deliberately, e.g. read-through with write-through.

## Related
- [Caching basics](caching-basics.md)
- [Write strategies](write-strategies.md)
- [Cache types](cache-types.md)
