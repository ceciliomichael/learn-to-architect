# Module 03 Exercise Solution

```sql
SELECT 
  item_name, 
  price, 
  discount_price 
FROM inventory 
WHERE (category = 'Electronics' OR price < 20.00) 
  AND discount_price IS NOT NULL;
```

### Expected Output

```text
┌────────────────┬───────┬────────────────┐
│   item_name    │ price │ discount_price │
├────────────────┼───────┼────────────────┤
│ Wireless Mouse │ 25.0  │ 20.0           │
│ Desk Pad       │ 15.0  │ 12.5           │
└────────────────┴───────┴────────────────┘
```

## Explanation

1. `(category = 'Electronics' OR price < 20.00)` combines two potential conditions with parentheses to preserve evaluation order.
2. `AND discount_price IS NOT NULL` requires that rows must have a non-null `discount_price`.
