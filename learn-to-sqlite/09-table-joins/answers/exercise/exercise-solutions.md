# Module 09 Exercise Solution

```sql
SELECT c.name, o.amount
FROM customers c
INNER JOIN orders o ON c.id = o.customer_id
WHERE o.amount > 50.0;
```

### Expected Output

```text
┌───────┬────────┐
│ name  │ amount │
├───────┼────────┤
│ Alice │ 150.0  │
│ Bob   │ 89.0   │
└───────┴────────┘
```

## Explanation

1. `INNER JOIN` filters out Charlie because Charlie has no orders.
2. `WHERE o.amount > 50.0` excludes Alice's order of 45.0.
