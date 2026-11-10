# Primary, foreign and composite keys

> A primary key uniquely identifies each row (no duplicates, no NULL). A foreign key is another table's primary key stored here to link the two. A composite key uses several columns together as the unique identifier.

studied: 2026-11-10 · status: done · source: SQL.pdf (pp. 4–5)

## Key ideas
- **Primary key (PK):**
  - the column that can **uniquely identify a row** in a table
  - **no duplicates** and **no NULL**
- **Foreign key (FK):**
  - a column holding the **primary key of another table**
  - this is how two tables are linked
- **Composite primary key:**
  - **multiple columns together** form the unique identifier
  - used when no single column is unique on its own

## Example
```sql
CREATE TABLE students (
  student_id  INT PRIMARY KEY,          -- PK
  name        VARCHAR(100)
);

CREATE TABLE courses (
  course_id   INT PRIMARY KEY,
  title       VARCHAR(100)
);

CREATE TABLE enrollments (
  student_id  INT,
  course_id   INT,
  grade       VARCHAR(2),
  PRIMARY KEY (student_id, course_id),                     -- composite PK
  FOREIGN KEY (student_id) REFERENCES students(student_id), -- FK
  FOREIGN KEY (course_id)  REFERENCES courses(course_id)    -- FK
);
```
```
enrollments
student_id | course_id | grade
    1      |    10     |  A     ✓
    1      |    11     |  B     ✓  (same student, different course)
    1      |    10     |  C     ✗  (pair (1,10) already exists)
```

## Pitfalls
- In a composite key only the **combination** has to be unique. Each column alone can repeat.
- A foreign key points at the other table's **primary key**, not at any column you like.
- A primary key can't be NULL, even when it's a composite key.

## Related
- [Constraints](constraints.md)
- [SQL data types](data-types.md)
- [Indexing vs sharding](../../backend/databases/indexing-and-sharding.md)
