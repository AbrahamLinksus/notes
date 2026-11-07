# N+1 query problem

> N+1 means one query to fetch N parent rows, then N more queries for each one's children. The fix is to load the children together, with a JOIN (eager loading) or a batch fetch.

studied: 2026-11-07 · status: done · source: Backend.pdf (p. 12)

## Key ideas
- It's a common **DB performance anti-pattern**:
  - the app runs **1 initial query** to fetch a list of parent records
  - then **N subsequent queries** to fetch related child data, one per record
- The total is N + 1 round trips. That's fine at N = 3 and terrible at N = 10,000.
- It often hides behind ORMs and GraphQL resolvers, where each `.children` access looks innocent.
- **Solutions:**
  1. **SQL joins (eager loading):** fetch parents and children in one query.
  2. **Batch fetching / data loaders:** collect all parent IDs, then fetch the children in one `IN (...)` query.

## Example
```python
# N+1: 1 + N queries
authors = db.query("SELECT * FROM authors")                  # 1
for a in authors:
    a.books = db.query("SELECT * FROM books WHERE author_id = ?", a.id)  # N
```
```sql
-- Fix 1: eager loading with a JOIN (1 query)
SELECT a.*, b.* FROM authors a LEFT JOIN books b ON b.author_id = a.id;
```
```python
# Fix 2: batch fetch (2 queries total)
ids = [a.id for a in authors]
books = db.query("SELECT * FROM books WHERE author_id IN (...)", ids)
# group books by author_id in memory
```
100 authors: 101 queries → 1 or 2.

## Pitfalls
- It doesn't show up in dev with 5 rows. It shows up in prod with 50,000.
- An eager JOIN on a one-to-many relation multiplies rows, so watch the payload size.
- GraphQL makes this especially easy to hit. Data loaders exist for exactly that case.

## Related
- [ORM](orm.md)
- [API styles overview](../apis/api-styles-overview.md)
- [Indexing and sharding](indexing-and-sharding.md)
