# SQL data types

> Every column is declared with a data type, and the core set covers whole numbers (INT, BIGINT), text (VARCHAR(n), TEXT), time (DATE, DATETIME), true/false (BOOLEAN) and exact decimals (DECIMAL).

studied: 2026-11-10 · status: done · source: SQL.pdf (p. 4)

## Key ideas
- The common column types, by what they hold:
  - **Whole numbers:** `INT`, `BIGINT` (for bigger ranges)
  - **Text:** `VARCHAR(n)` (up to *n* characters), `TEXT` (long free text)
  - **Time:** `DATE` (day only), `DATETIME` (day and time)
  - **True/false:** `BOOLEAN`
  - **Exact numbers with decimals:** `DECIMAL`
- The type decides what values the column accepts, so pick the narrowest type that fits the data.

## Example
```sql
CREATE TABLE orders (
  id          BIGINT,           -- grows forever → BIGINT
  qty         INT,
  customer    VARCHAR(100),     -- short text with a known max length
  notes       TEXT,             -- long free text
  order_date  DATE,             -- 2026-11-10
  shipped_at  DATETIME,         -- 2026-11-10 14:32:00
  is_paid     BOOLEAN,
  amount      DECIMAL(10, 2)    -- money: 12345678.90
);
```

## Pitfalls
- `VARCHAR` needs its length `n`. Text longer than `n` won't fit.
- Use `DATE` when you only care about the day, and `DATETIME` when the time matters too.
- Store money in `DECIMAL`, which is exact, rather than a floating-point type.

## Related
- [Keys](keys.md)
- [Constraints](constraints.md)
