# Module 09 Exercise Solution

```sql
SELECT c.`name` AS `inactive_customer`
FROM `customers` c
LEFT JOIN `orders` o ON c.`id` = o.`customer_id`
WHERE o.`id` IS NULL;
```

### Expected Output

```text
+-------------------+
| inactive_customer |
+-------------------+
| Charlie           |
+-------------------+
```

## Explanation

1. `LEFT JOIN` preserves all customer records.
2. `WHERE o.id IS NULL` filters out any customer who has order records, identifying customers without orders.
