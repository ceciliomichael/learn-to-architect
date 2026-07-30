# Module 04 Exercise Solution

```sql
SELECT `title`, `unit_price` 
FROM `items` 
ORDER BY `unit_price` DESC 
LIMIT 1 OFFSET 1;
```

### Expected Output

```text
+--------------------+------------+
| title              | unit_price |
+--------------------+------------+
| Ergonomic Keyboard |     129.99 |
+--------------------+------------+
```

## Explanation

1. `ORDER BY unit_price DESC` places 4K Monitor (349.50) first and Ergonomic Keyboard (129.99) second.
2. `OFFSET 1` skips the 1st row (349.50) and `LIMIT 1` returns the 2nd row (129.99).
