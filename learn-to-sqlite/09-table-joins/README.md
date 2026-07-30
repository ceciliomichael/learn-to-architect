# Module 09: Connect Data with Joins

## What You Will Learn

In this module, you will learn how to query data spanning multiple related tables using `INNER JOIN`, `LEFT JOIN`, and `CROSS JOIN`, qualify column names using table aliases, and model normalized relational relationships.

---

## Types of Joins

- **`INNER JOIN`**: Returns rows only when there is a matching key in **both** tables.
- **`LEFT JOIN`** (or `LEFT OUTER JOIN`): Returns **all** rows from the left table, plus matched rows from the right table. Unmatched right side fields return `NULL`.
- **`CROSS JOIN`**: Produces a Cartesian product (combines every left row with every right row).

```sql
SELECT orders.id, customers.name, orders.amount
FROM orders
INNER JOIN customers ON orders.customer_id = customers.id;
```

---

## Step-by-Step Practical Example

```sql
CREATE TABLE customers (
  id INTEGER PRIMARY KEY,
  name TEXT NOT NULL
);

CREATE TABLE orders (
  id INTEGER PRIMARY KEY,
  customer_id INTEGER,
  amount REAL NOT NULL
);

INSERT INTO customers VALUES (1, 'Alice'), (2, 'Bob'), (3, 'Charlie');
INSERT INTO orders VALUES (101, 1, 150.0), (102, 1, 45.0), (103, 2, 89.0);

-- LEFT JOIN shows Charlie (who has no orders) with NULL amount
SELECT c.name, o.id AS order_id, o.amount
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id;
```

### Output

```text
┌─────────┬──────────┬────────┐
│  name   │ order_id │ amount │
├─────────┼──────────┼────────┤
│ Alice   │ 101      │ 150.0  │
│ Alice   │ 102      │ 45.0   │
│ Bob     │ 103      │ 89.0   │
│ Charlie │          │        │
└─────────┴──────────┴────────┘
```

---

## Check Your Understanding

1. What happens to right-side columns when a `LEFT JOIN` finds no matching foreign key row?
2. How do table aliases (`customers c`) simplify query writing?
