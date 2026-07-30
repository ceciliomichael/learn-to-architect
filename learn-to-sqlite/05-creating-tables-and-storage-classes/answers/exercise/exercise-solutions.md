# Module 05 Exercise Solution

```sql
CREATE TABLE products_strict (
  product_id INT PRIMARY KEY,
  title TEXT NOT NULL,
  price REAL NOT NULL
) STRICT;

-- Valid rows
INSERT INTO products_strict VALUES (1, 'Desk Chair', 149.99);
INSERT INTO products_strict VALUES (2, 'Desk Lamp', 29.50);

-- Invalid row (will throw: Runtime error: cannot store TEXT value in REAL column products_strict.price)
INSERT INTO products_strict VALUES (3, 'Monitor', 'expensive');
```

## Explanation

1. `STRICT` forces SQLite to validate column data types upon insertion.
2. Inserting `'expensive'` into column `price` (declared `REAL`) causes immediate rejection.
