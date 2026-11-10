# Constraints

> Constraints are column rules the DB enforces on every insert: AUTO_INCREMENT fills IDs, NOT NULL makes a value mandatory, UNIQUE blocks duplicates, CHECK validates a condition, and DEFAULT supplies a fallback value.

studied: 2026-11-10 · status: done · source: SQL.pdf (pp. 5–6)

## Key ideas
1. **AUTO_INCREMENT:**
   - the column has to be a **primary key or unique key**
   - each new row gets **last entry + 1**
2. **NOT NULL:** makes the value **mandatory** on insert.
3. **UNIQUE:** **blocks duplicates** in the column.
4. **CHECK (condition):**
   - checks a condition for **validation before insert**
   - the constraint **has a name**
5. **DEFAULT:** a **fallback value** used when nothing is inserted for that column.

## Example
```sql
CREATE TABLE users (
  id       INT AUTO_INCREMENT PRIMARY KEY,
  email    VARCHAR(100) NOT NULL UNIQUE,
  age      INT,
  country  VARCHAR(50) DEFAULT 'India',
  CONSTRAINT chk_age CHECK (age >= 18)        -- named CHECK
);

INSERT INTO users (email, age) VALUES ('a@x.com', 21);
-- → id = 1 (auto), country = 'India' (default)

INSERT INTO users (email, age) VALUES ('a@x.com', 25);
-- ✗ UNIQUE: email already exists

INSERT INTO users (age) VALUES (30);
-- ✗ NOT NULL: email missing

INSERT INTO users (email, age) VALUES ('b@x.com', 15);
-- ✗ CHECK chk_age fails
```

## Pitfalls
- AUTO_INCREMENT only works on a primary or unique key column.
- DEFAULT only applies when the column is **left out** of the insert. An explicit NULL is not "nothing inserted".
- Naming a CHECK constraint makes the error readable and lets you drop it by name later.

## Related
- [Keys](keys.md)
- [NULL handling](../queries/null-handling.md)
- [ACID properties](../../backend/databases/acid-properties.md)
