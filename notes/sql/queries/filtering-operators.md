# Filtering operators

> Beyond plain `=`, WHERE can test for NULL (IS NULL), list membership (IN), ranges (BETWEEN) and text patterns (LIKE with `%` and `_`). Each one has a NOT version.

studied: 2026-11-10 · status: done · source: SQL.pdf (pp. 8–9)

## Key ideas
- **IS NULL / IS NOT NULL:** checks whether a field is NULL. NULL is not `0` or `""`.
- **IN / NOT IN:** checks whether a value matches something in a given list.
- **BETWEEN / NOT BETWEEN:** checks whether a value lies within a range.
- **LIKE / NOT LIKE:** pattern matching.
  - `%` → any sequence of characters (including none)
  - `_` → exactly one character
  - to match a literal `_`, escape it as `\_`

## Example
```sql
-- IN
SELECT * FROM users WHERE city IN ('Chennai', 'Coimbatore');

-- BETWEEN (range)
SELECT * FROM orders WHERE amount BETWEEN 100 AND 500;

-- LIKE
SELECT * FROM users WHERE name LIKE 'Ra%';      -- Ravi, Rahul, Ra
SELECT * FROM users WHERE name LIKE 'R_vi';     -- Ravi (exactly one char in the gap)
SELECT * FROM files WHERE name LIKE 'test\_%';  -- test_1.py, not test1.py

-- IS NULL
SELECT * FROM users WHERE phone IS NOT NULL;
```

## Pitfalls
- In LIKE, `_` is a wildcard. Searching for `'test_%'` also matches `test1.py`. Use `\_` for a real underscore.
- `%` matches zero characters too, so `'Ra%'` matches `'Ra'` itself.
- `= NULL` never matches anything. Use `IS NULL`.

## Related
- [Basic SELECT clauses](basic-select-clauses.md)
- [NULL handling](null-handling.md)
- [CASE expressions](case-expressions.md)
