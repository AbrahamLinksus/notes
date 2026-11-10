# NULL handling

> NULL means "no value" or "unknown". It is not 0 and not an empty string, so you test for it with IS NULL and replace it with IFNULL or COALESCE.

studied: 2026-11-10 · status: done · source: SQL.pdf (pp. 6, 8–10)

## Key ideas
- **NULL** = "no value" or "unknown". It means the value **doesn't exist**.
  - It is **not `0`** and **not `""`** (empty string).
- **Checking for NULL:** use `IS NULL` / `IS NOT NULL` to test whether a field is NULL.
- **NULL spreads through functions:**
  - `ROUND(NULL)` → NULL
  - `GREATEST(...)` / `LEAST(...)` with any NULL argument → NULL
- **Replacing NULL:**
  - `IFNULL(value, replacement)`: returns `value` if it is not NULL, otherwise `replacement`.
  - `COALESCE(v1, v2, …)`: returns the **first non-NULL** value in the list.

## Example
```
employees
name  | phone      | email
Asha  | NULL       | asha@x.com
Ravi  | 98400xxxxx | NULL
Meena | NULL       | NULL
```
```sql
SELECT name FROM employees WHERE phone IS NULL;
-- Asha, Meena

SELECT name, IFNULL(phone, 'no phone') FROM employees;
-- Asha → 'no phone', Ravi → 98400xxxxx, Meena → 'no phone'

SELECT name, COALESCE(phone, email, 'no contact') AS contact FROM employees;
-- Asha → asha@x.com, Ravi → 98400xxxxx, Meena → 'no contact'
```

## Pitfalls
- `WHERE phone = NULL` doesn't find NULLs. Always use `IS NULL`.
- Treating NULL as 0 or `''`: a NULL salary is "unknown", not "zero".
- One NULL argument makes `GREATEST`/`LEAST` return NULL. Wrap the arguments in `COALESCE` first if that's not what you want.
- `IFNULL` takes exactly one fallback. `COALESCE` can try several in order.

## Related
- [Constraints](../schema/constraints.md)
- [Filtering operators](filtering-operators.md)
- [Scalar functions](scalar-functions.md)
- [CASE expressions](case-expressions.md)
