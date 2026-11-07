# Indexing vs sharding

> An index is an extra data structure that makes lookups on one table fast. Sharding splits a huge database into non-overlapping pieces across machines, which is horizontal scaling.

studied: 2026-11-07 · status: done · source: Backend.pdf (p. 33)

## Key ideas
- **Index:**
  - a data structure built on top of a table to **speed up data retrieval**
  - created using **B-trees** or **LSM trees**
  - it speeds up reads without changing what data you have
- **Sharding:**
  - splits a huge DB into **multiple non-overlapping DBs** called **shards**
  - lets you **store more data** and **reduce latency**, since each shard is smaller and serves part of the load
  - it's a form of **horizontal scaling**: more machines, not a bigger machine
- They solve different problems:
  - **index:** "this query is slow on a table that fits on one machine"
  - **sharding:** "the data or traffic doesn't fit on one machine"

## Example
Index:
```sql
-- without index: scan every row for email
SELECT * FROM users WHERE email = 'a@x.com';
CREATE INDEX idx_users_email ON users(email);   -- B-tree → log-time lookup
```
Sharding by user ID:
```
shard = user_id % 3
  shard 0: users 3, 6, 9 …
  shard 1: users 1, 4, 7 …
  shard 2: users 2, 5, 8 …     (no row lives in two shards)
query for user 7 → shard 1 only
```

## Pitfalls
- Indexes aren't free: every write must also update the index, and they take space.
- Queries that span shards (e.g. joins across users) become hard and slow.
- Re-sharding with plain modulo moves most rows. That's the same problem consistent hashing solves for caches.

## Related
- [N+1 problem](n-plus-one-problem.md)
- [Database migrations](database-migrations.md)
- [Cache types](../caching/cache-types.md)
- [Monolith vs microservices](../architecture/monolith-vs-microservices.md)
