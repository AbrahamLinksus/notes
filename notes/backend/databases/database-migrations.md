# Database migrations

> A migration is a controlled change to a database. Schema migrations change its structure step by step, and data migrations move data from one DB to another.

studied: 2026-11-07 · status: done · source: Backend.pdf (p. 9)

## Key ideas
- **Two types:**
  1. **Schema migration:** **incremental** changes to the DB schema, like adding or modifying tables, columns, indexes or constraints.
  2. **Data migration:** **moving data** from one database to another.
- Schema migrations are small, ordered steps. Each one builds on the previous schema version, so every environment can be brought to the same state by replaying them.

## Example
Schema migration, one incremental step:
```sql
-- 003_add_phone_to_users.sql
ALTER TABLE users ADD COLUMN phone VARCHAR(20);
CREATE INDEX idx_users_phone ON users(phone);
```
Applied in order:
```
001_create_users → 002_create_orders → 003_add_phone_to_users
dev DB:  at 003 ✔      prod DB: at 002 → run 003 → ✔ in sync
```
Data migration:
```
old MySQL `customers`  ──export/transform──►  new Postgres `users`
```

## Pitfalls
- Editing a migration that has already run elsewhere. Add a new incremental one instead.
- Confusing the two types: changing a column type is schema, copying rows between systems is data.
- Running a schema change on a huge table without checking whether it locks the table.

## Related
- [ORM](orm.md)
- [Indexing and sharding](indexing-and-sharding.md)
- [CI/CD](../devops/ci-cd.md)
