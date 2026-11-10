# Basic SELECT clauses

> A basic query answers one question per clause: SELECT which columns, FROM which table, WHERE which rows, ORDER BY how to sort, LIMIT/OFFSET how many, DISTINCT whether to drop duplicates, and AS what to call things.

studied: 2026-11-10 · status: done · source: SQL.pdf (p. 7)

## Key ideas
1. **SELECT:** which columns to show.
2. **FROM:** which table to read from.
3. **WHERE:** which rows to keep.
4. **ORDER BY:** how to sort.
5. **LIMIT / OFFSET:** how many rows to return (and how many to skip).
6. **DISTINCT:** whether to remove duplicates.
7. **AS (alias):** renames a column or table in the output.

## Example
```
products
id | name    | category | price
1  | Pen     | Stationery | 20
2  | Notebook| Stationery | 60
3  | Mouse   | Electronics| 500
4  | Cable   | Electronics| 150
5  | Eraser  | Stationery | 10
```
```sql
SELECT name AS product, price          -- columns (name renamed)
FROM products                          -- table
WHERE category = 'Stationery'          -- keep only these rows
ORDER BY price DESC                    -- sort high → low
LIMIT 2 OFFSET 0;                      -- top 2
```
```
product  | price
Notebook | 60
Pen      | 20
```
```sql
SELECT DISTINCT category FROM products;
-- Stationery, Electronics   (duplicates removed)
```

## Pitfalls
- Without `ORDER BY`, `LIMIT` returns an arbitrary set of rows. Sort first when you want the "top N".
- `DISTINCT` applies to the **whole selected row**, not just the first column.
- `OFFSET n` skips n rows, so page 3 with 10 per page is `LIMIT 10 OFFSET 20`.

## Related
- [Filtering operators](filtering-operators.md)
- [NULL handling](null-handling.md)
- [Query lifecycle](../../backend/databases/query-lifecycle.md)
