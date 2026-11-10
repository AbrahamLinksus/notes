# OLTP vs OLAP

> A database's workload is the pattern of how it's used: OLTP handles many small day-to-day operations fast, while OLAP is built for analysis and big business decisions.

studied: 2026-11-10 · status: done · source: SQL.pdf (p. 2)

## Key ideas
- **Workload:** the pattern of how a DB is used. Workloads fall into two groups.
- **OLTP (Online Transaction Processing):**
  - handles **day-to-day operations**
  - goal is **speed on high volume**
  - typical load: **small, frequent queries**
- **OLAP (Online Analytical Processing):**
  - built for **analysis** and making **big business decisions**
  - typical use: **finding trends**
- Ask: "Is this DB running the business right now (OLTP), or studying how the business went (OLAP)?"

## Example
```
OLTP — an online store, every second:
  INSERT INTO orders (user_id, item_id) VALUES (7, 301);
  UPDATE stock SET qty = qty - 1 WHERE item_id = 301;
  → tiny, frequent, must be fast

OLAP — the same store, once a month:
  SELECT region, month, SUM(amount)
  FROM orders
  GROUP BY region, month;
  → one big scan over lots of history to find trends
```

## Pitfalls
- Running heavy analysis queries on the live OLTP database can slow down the small, frequent queries it exists to serve.
- "Online" is in both names. The real difference is transactions (OLTP) vs analysis (OLAP).

## Related
- [Transactions and concurrency](transactions-and-concurrency.md)
- [Database storage internals](database-storage-internals.md)
- [Indexing vs sharding](indexing-and-sharding.md)
