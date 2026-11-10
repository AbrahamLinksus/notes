# Query lifecycle

> Every SQL query goes through three internal steps: parse (is the syntax correct?), plan (what's the fastest way to run it?), and execute (run that plan).

studied: 2026-11-10 · status: done · source: SQL.pdf (p. 6)

## Key ideas
- When a SQL query is run, internally it follows a lifecycle:
  1. **Parse:** checks that the SQL is written **syntactically correctly**.
  2. **Plan** (also called **query optimization**): the DB figures out how to execute the query in the **fastest / most efficient way**.
  3. **Execute:** runs the plan.
- The plan step is where indexes matter: the planner decides whether to use one (B-tree / B+ tree / hash) or to scan the whole table.

## Example
```sql
SELECT name FROM users WHERE email = 'a@x.com';
```
```
PARSE    → keywords, commas and quotes are valid?   ✓
           (a typo like "SELEC name" fails here, before anything runs)

PLAN     → option 1: scan every row of users
           option 2: use the index on email → jump to the row
           → picks option 2 (cheaper)

EXECUTE  → follow the index, read that page, return name
```

## Pitfalls
- A query can parse fine and still be slow. That's a plan problem (e.g. no useful index), not a syntax problem.
- Mixing up parse errors and run-time errors: syntax is caught at parse time, while missing data or constraint violations only show up during execute.

## Related
- [Indexing vs sharding](indexing-and-sharding.md)
- [Database storage internals](database-storage-internals.md)
- [Basic SELECT clauses](../../sql/queries/basic-select-clauses.md)
