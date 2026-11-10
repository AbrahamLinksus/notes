# Transactions and concurrency

> A transaction is a bundle of operations that must succeed or fail as one unit. The DB protects it with a transaction log for crashes and with locks or MVCC so others don't see half-finished work.

studied: 2026-11-10 · status: done · source: SQL.pdf (pp. 2–3)

## Key ideas
- **Transaction:** a bundle of operations that logically belong together and must behave as **one unit**.
  - Either **everything** in the bundle succeeds, or **nothing** does.
- **Transactional databases** enforce this in two ways:
  1. **Transaction log:**
     - before making real changes, the DB **writes the intended changes into the log**
     - if the system crashes, the log tells it whether the transaction **completed** or not
  2. **Isolation (locks and MVCC):**
     - **Lock:** while one person is modifying data, **no one else can access** the half-finished work.
     - **MVCC (multi-version concurrency control):** the DB keeps the **previous version** of the data visible until the new changes are **confirmed**.

## Example
Bank transfer of ₹500 from A to B:
```sql
BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE id = 'A';
UPDATE accounts SET balance = balance + 500 WHERE id = 'B';
COMMIT;
```
```
1. log: "A −500, B +500"   ← written first
2. apply A −500
   ✗ crash here → on restart the log shows the transaction never completed
                → nothing is kept, so A doesn't lose the money

Meanwhile another reader:
  with a lock → waits until COMMIT
  with MVCC   → sees the old balances until COMMIT, never the halfway state
```

## Pitfalls
- Two related updates sent without a transaction can leave the data half-changed if anything fails in between.
- Locks make others wait. MVCC lets readers continue, but they see the old version until commit, not the new one.

## Related
- [ACID properties](acid-properties.md)
- [OLTP vs OLAP](oltp-vs-olap.md)
- [Idempotency](../architecture/idempotency.md)
