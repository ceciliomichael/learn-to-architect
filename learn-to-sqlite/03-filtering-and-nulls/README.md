# Module 03: Filter Rows and Master Three-Valued Logic (`NULL`)

## What You Will Learn

In this module, you will master filtering query results using the `WHERE` clause, comparing values with `=`, `!=`, `<`, `>`, `BETWEEN`, `IN`, and `LIKE`, and understanding SQLite's three-valued logic when dealing with missing values (`NULL`).

---

## Filtering Rows with `WHERE`

The `WHERE` clause filters rows *before* they are returned by `SELECT`. Only rows that evaluate to `TRUE` for the filter condition are included.

```sql
SELECT title, price FROM books WHERE price > 20.00;
```

### Common Comparison Operators

| Operator | Meaning | Example |
| :--- | :--- | :--- |
| `=` | Equals | `category = 'Fiction'` |
| `!=` or `<>` | Not equals | `status != 'Archived'` |
| `<`, `>` | Less than, Greater than | `stock < 5` |
| `BETWEEN a AND b` | Inclusive range | `price BETWEEN 10.00 AND 25.00` |
| `IN (a, b, c)` | Value in list | `city IN ('Tokyo', 'Paris', 'London')` |
| `LIKE 'pattern'` | Pattern matching (`%` multi-char, `_` single char) | `email LIKE '%@gmail.com'` |

---

## Three-Valued Logic and `NULL`

In relational databases, `NULL` represents **unknown or missing information**.

Because `NULL` is unknown, comparing anything to `NULL` using `=` or `!=` evaluates to **`UNKNOWN`** (neither `TRUE` nor `FALSE`).

```sql
-- WRONG (Returns zero rows because NULL = NULL is UNKNOWN)
SELECT * FROM users WHERE middle_name = NULL;

-- CORRECT (Checks if value is missing)
SELECT * FROM users WHERE middle_name IS NULL;

-- CORRECT (Checks if value exists)
SELECT * FROM users WHERE middle_name IS NOT NULL;
```

### The `COALESCE()` Function

`COALESCE(val1, val2, ...)` evaluates arguments in order and returns the **first non-NULL value**:

```sql
SELECT title, COALESCE(discount_price, list_price) AS final_price FROM products;
```

---

## Step-by-Step Practical Example

```sql
CREATE TABLE inventory (
  id INTEGER PRIMARY KEY,
  item_name TEXT NOT NULL,
  category TEXT NOT NULL,
  price REAL NOT NULL,
  discount_price REAL
);

INSERT INTO inventory VALUES
  (1, 'Wireless Mouse', 'Electronics', 25.00, 20.00),
  (2, 'Mechanical Keyboard', 'Electronics', 85.00, NULL),
  (3, 'Desk Pad', 'Office', 15.00, 12.50),
  (4, 'USB-C Cable', 'Electronics', 10.00, NULL);

SELECT 
  item_name, 
  price, 
  COALESCE(discount_price, price) AS effective_price 
FROM inventory 
WHERE category = 'Electronics' AND discount_price IS NULL;
```

### Output

```text
┌─────────────────────┬───────┬─────────────────┐
│      item_name      │ price │ effective_price │
├─────────────────────┼───────┼─────────────────┤
│ Mechanical Keyboard │ 85.0  │ 85.0            │
│ USB-C Cable         │ 10.0  │ 10.0            │
└─────────────────────┴───────┴─────────────────┘
```

### Line-by-Line Breakdown

- `WHERE category = 'Electronics'`: Limits initial candidate rows to items in the Electronics category.
- `AND discount_price IS NULL`: Filters down to only those items where `discount_price` has no value recorded (`NULL`).
- `COALESCE(discount_price, price)`: If `discount_price` were non-null it would return it, otherwise falls back to `price`.

---

## Common Beginner Mistakes & Solutions

### 1. Writing `WHERE column = NULL`
- **Cause**: Assuming `NULL` is a concrete value that equals itself.
- **Fix**: Always use `IS NULL` or `IS NOT NULL`.

---

## Check Your Understanding

1. Why does `SELECT * FROM inventory WHERE price = NULL;` produce an empty result set?
2. How does `COALESCE('A', 'B')` differ from `COALESCE(NULL, 'B')`?
