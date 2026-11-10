# Scalar functions: ROUND, ABS, GREATEST, LEAST

> Scalar functions work value by value: ROUND trims to a number of decimals (0 by default), ABS drops the sign, and GREATEST/LEAST pick the largest or smallest of their arguments. Any NULL input gives NULL.

studied: 2026-11-10 · status: done · source: SQL.pdf (p. 9)

## Key ideas
- **`ROUND(value, decimal)`:**
  - rounds a number to the given number of decimals
  - `decimal` is **optional** and **defaults to 0**, which gives an integer
  - a NULL value returns **NULL**
- **`ABS(value)`:** returns the **absolute value**.
- **`GREATEST(...)` / `LEAST(...)`:**
  - takes *n* values as parameters and returns the **largest / smallest**
  - if **any** argument is NULL, the result is **NULL**
- These compare values **across columns in one row**. They don't work down a column.

## Example
```sql
SELECT ROUND(3.14159, 2);     -- 3.14
SELECT ROUND(3.6);            -- 4      (default 0 decimals)
SELECT ROUND(NULL, 2);        -- NULL

SELECT ABS(-42);              -- 42

SELECT GREATEST(10, 50, 30);  -- 50
SELECT LEAST(10, 50, 30);     -- 10
SELECT GREATEST(10, NULL, 30);-- NULL
```
Per row:
```
marks: name | test1 | test2 | test3
       Asha |  70   |  85   |  60
SELECT name, GREATEST(test1, test2, test3) AS best FROM marks;
-- Asha | 85
```

## Pitfalls
- `GREATEST` (one row, across columns) is different from `MAX` (aggregate, down one column).
- One NULL score makes `GREATEST`/`LEAST` NULL. Use `COALESCE(test2, 0)` if a missing score should count as 0.
- `ROUND(x)` with no second argument gives a whole number, not "unchanged".

## Related
- [NULL handling](null-handling.md)
- [CASE expressions](case-expressions.md)
