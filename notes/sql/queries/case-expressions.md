# CASE expressions

> CASE lets SQL evaluate conditions and return a value based on business rules. A searched CASE uses boolean conditions (good for thresholds), and a simple CASE compares one value for equality.

studied: 2026-11-10 · status: done · source: SQL.pdf (pp. 10–11)

## Key ideas
- **CASE** evaluates conditions and returns values based on defined **business rules**.
- It's an **expression**, so it **returns a value** and can go anywhere a value can (SELECT, ORDER BY, …).
- Syntax:
  ```
  CASE
    WHEN condition THEN result
    WHEN condition THEN result
    ELSE result
  END
  ```
- Two forms:
  1. **Searched CASE:** each `WHEN` is a **boolean condition**. Needed for **thresholds** and ranges.
  2. **Simple CASE:** compares one expression for **direct equality**.

## Example
Searched CASE (thresholds):
```sql
SELECT name, marks,
  CASE
    WHEN marks >= 90 THEN 'A'
    WHEN marks >= 75 THEN 'B'
    WHEN marks >= 50 THEN 'C'
    ELSE 'Fail'
  END AS grade
FROM students;
-- 92 → A, 80 → B, 40 → Fail
```
Simple CASE (equality):
```sql
SELECT order_id,
  CASE status
    WHEN 'P' THEN 'Pending'
    WHEN 'S' THEN 'Shipped'
    WHEN 'D' THEN 'Delivered'
    ELSE 'Unknown'
  END AS status_label
FROM orders;
```

## Pitfalls
- `WHEN`s are checked **top to bottom** and the first match wins. Put the strictest threshold first (`>= 90` before `>= 75`).
- Without `ELSE`, rows that match nothing get **NULL**.
- Simple CASE can only test equality. For `>`, `<` or ranges, use searched CASE.
- Don't forget `END`. It closes the expression.

## Related
- [NULL handling](null-handling.md)
- [Scalar functions](scalar-functions.md)
- [Filtering operators](filtering-operators.md)
