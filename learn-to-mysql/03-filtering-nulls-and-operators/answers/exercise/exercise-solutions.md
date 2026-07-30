# Module 03 Exercise Solution

```sql
SELECT 
  `title`,
  `unit_price`,
  IFNULL(`discount_price`, `unit_price`) AS `effective_price`
FROM `items`
WHERE `unit_price` BETWEEN 100.00 AND 400.00;
```

### Expected Output

```text
+--------------------+------------+-----------------+
| title              | unit_price | effective_price |
+--------------------+------------+-----------------+
| Ergonomic Keyboard |     129.99 |          129.99 |
| 4K Monitor         |     349.50 |          349.50 |
+--------------------+------------+-----------------+
```

## Explanation

1. `BETWEEN 100.00 AND 400.00` filters for inclusive prices within range.
2. `IFNULL(discount_price, unit_price)` returns `discount_price` if non-null, else `unit_price`.
