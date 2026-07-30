# Module 04: Sort, Remove Duplicates, and Limit Results

## What You Will Learn

In this module, you will learn how to control the order of returned rows using `ORDER BY`, eliminate duplicate result rows with `DISTINCT`, and constrain the number of returned rows using `LIMIT` and `OFFSET`.

---

## Ordering Results (`ORDER BY`)

Without an explicit `ORDER BY` clause, a database engine does **not** guarantee any specific row sequence.

```sql
SELECT name, price FROM products ORDER BY price DESC;
```

- `ASC`: Ascending order (default, e.g. A to Z, 1 to 100).
- `DESC`: Descending order (e.g. Z to A, 100 to 1).

### Sorting by Multiple Columns

```sql
SELECT category, name, price FROM products ORDER BY category ASC, price DESC;
```

---

## Removing Duplicates (`DISTINCT`)

The `DISTINCT` keyword removes duplicate rows from query results:

```sql
SELECT DISTINCT category FROM products;
```

---

## Pagination with `LIMIT` and `OFFSET`

- `LIMIT n`: Restricts the output set to `n` rows.
- `OFFSET m`: Skips the first `m` rows before returning output.

```sql
-- Get page 2 of products (rows 11-20, skipping first 10)
SELECT id, name, price FROM products ORDER BY id ASC LIMIT 10 OFFSET 10;
```

---

## Step-by-Step Practical Example

```sql
CREATE TABLE scores (
  id INTEGER PRIMARY KEY,
  player TEXT NOT NULL,
  score INTEGER NOT NULL
);

INSERT INTO scores VALUES
  (1, 'Alice', 450),
  (2, 'Bob', 520),
  (3, 'Charlie', 450),
  (4, 'Diana', 610),
  (5, 'Eve', 520);

-- Top 3 distinct high scores
SELECT DISTINCT score FROM scores ORDER BY score DESC LIMIT 3;
```

### Output

```text
┌───────┐
│ score │
├───────┤
│ 610   │
│ 520   │
│ 450   │
└───────┘
```

---

## Common Beginner Mistakes & Solutions

### 1. Using `LIMIT` without `ORDER BY`
- **Cause**: Expecting a deterministic "top 5" result without specifying sort criteria.
- **Fix**: Always specify `ORDER BY` whenever using `LIMIT`.

---

## Check Your Understanding

1. What happens if you use `OFFSET 5` without `LIMIT` in SQLite?
2. Why is row order non-deterministic when `ORDER BY` is omitted?
