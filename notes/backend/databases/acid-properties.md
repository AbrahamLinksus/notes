# ACID properties

> ACID is the set of guarantees a transactional DB gives: all-or-nothing, always valid, isolated from other transactions, and permanent once committed.

studied: 2026-11-10 · status: done · source: SQL.pdf (p. 3)

## Key ideas
- **Atomicity:** all or nothing. Every step in the transaction happens, or none does.
- **Consistency:** data stays **valid according to the business logic** (validation rules).
- **Isolation:** **single access at an instant**, so other transactions never touch half-finished work. In practice this is done with **locks** or **MVCC**.
- **Durability:** once a transaction is **committed**, its data is written **permanently** and survives a crash.
- How each one is enforced:
  - Atomicity and durability → the **transaction log**
  - Isolation → **locks / MVCC**
  - Consistency → **constraints** and validation rules

## Example
Transfer ₹500 from A (balance ₹300) to B, with the rule `CHECK (balance >= 0)`:
```
Atomicity    → if crediting B fails, A's debit is undone too
Consistency  → A would go to −200, breaks the CHECK → transaction rejected
Isolation    → someone reading A's balance mid-transfer never sees a halfway value
Durability   → after COMMIT succeeds, a power cut doesn't lose the transfer
```

## Pitfalls
- ACID consistency means "valid by the business rules". It's a different idea from consistency between replicas in distributed systems.
- Durability only starts at **commit**. Anything uncommitted can still be lost.

## Related
- [Transactions and concurrency](transactions-and-concurrency.md)
- [Constraints](../../sql/schema/constraints.md)
- [Database migrations](database-migrations.md)
