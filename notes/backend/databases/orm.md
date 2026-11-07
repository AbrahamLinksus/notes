# ORM (Object Relational Mapping)

> An ORM lets you work with the database through objects instead of raw SQL. That's convenient, but you pay in translation overhead, leaky abstraction and less control.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 28–29)

## Key ideas
- An **ORM** helps developers interact with a DB using **OOP concepts**: tables become classes and rows become objects.
- It's an **abstraction over SQL queries**. The ORM generates the SQL for you.
- **Examples:** Prisma; Sequelize (a TypeScript/Node.js ORM).
- **Drawbacks:**
  1. **Translation performance overhead:** object ↔ SQL conversion costs time.
  2. **Abstraction leak:** it hides how things work, until you need to know.
  3. **Less flexible** than handwritten SQL for complex queries.
  4. **Maintenance overhead:** one more layer and dependency to keep updated.
  5. **Complexity.**

## Example
Same query, both ways:
```ts
// Prisma (ORM)
const users = await prisma.user.findMany({
  where: { age: { gt: 21 } },
  include: { orders: true },
});
```
```sql
-- what you'd write by hand
SELECT u.*, o.*
FROM users u LEFT JOIN orders o ON o.user_id = u.id
WHERE u.age > 21;
```
An abstraction leak in practice: a loop that touches `user.orders` lazily can quietly fire one query per user, which is the N+1 problem.

## Pitfalls
- Trusting the ORM blindly: always check the SQL it generates for hot paths.
- Using the ORM for everything. Heavy reporting queries are often clearer and faster in raw SQL.
- Lazy loading inside loops leads to N+1.

## Related
- [N+1 problem](n-plus-one-problem.md)
- [Database migrations](database-migrations.md)
- [Indexing and sharding](indexing-and-sharding.md)
