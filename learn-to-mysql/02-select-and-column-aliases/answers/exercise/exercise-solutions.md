# Module 02 Exercise Solution

```sql
SELECT 
  CONCAT('ITEM: ', `title`, ' Costs $', `unit_price`) AS `price_tag`,
  `unit_price` * 0.85 AS `discount_price`
FROM `items`;
```

### Expected Output

```text
+------------------------------------+----------------+
| price_tag                          | discount_price |
+------------------------------------+----------------+
| ITEM: Ergonomic Keyboard Costs $129.99 |       110.4915 |
| ITEM: 4K Monitor Costs $349.50     |       297.0750 |
+------------------------------------+----------------+
```

## Explanation

1. `CONCAT()` joins all string and column arguments sequentially.
2. `+` operator in MySQL is exclusively arithmetic; string joining requires `CONCAT()`.
