# Database storage internals

> A database keeps rows in small fixed units called pages, moves them between disk and RAM as blocks, caches the hot ones in a buffer cache, and uses B-trees or hash structures to find them fast.

studied: 2026-11-10 · status: done · source: SQL.pdf (p. 1)

## Key ideas
- **Database:** an organized collection of **structured data**.
- For a **local DB**, the data lives on the **disk or SSD** of that machine.
- **How it's stored:**
  1. **Pages:** rows are stored inside small units called pages.
  2. **Blocks:** pages move between **secondary memory (disk)** and **primary memory (RAM)** as blocks.
  3. **Caching:** frequently used data is kept in a **buffer cache** in RAM, so it doesn't have to be read from disk again.
- **How it's searched efficiently:**
  - **B-trees / B+ trees**
  - **hash structures**

## Example
```
SELECT * FROM users WHERE id = 42;

1. B+ tree on id  → tells the DB which page holds id 42
2. page in buffer cache?
      yes → read it straight from RAM      (fast)
      no  → load that block from disk/SSD  (slow)
            → keep it in the buffer cache for next time
3. find row 42 inside the page → return it
```

## Pitfalls
- The DB doesn't read single rows from disk. It reads whole pages, so a query that touches one row still pulls in its whole page.
- The buffer cache lives in RAM. It only helps for data that is used often; cold data still costs a disk read.
- Disk/SSD is where the data actually lives. The cache is only a copy.

## Related
- [Indexing vs sharding](indexing-and-sharding.md)
- [Query lifecycle](query-lifecycle.md)
- [OLTP vs OLAP](oltp-vs-olap.md)
- [Caching basics](../caching/caching-basics.md)
