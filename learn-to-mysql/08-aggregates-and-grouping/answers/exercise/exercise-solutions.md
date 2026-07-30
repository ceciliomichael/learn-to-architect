# Module 08 Exercise Solution

```sql
SELECT 
  `region`, 
  SUM(`amount`) AS `total_revenue`
FROM `sales`
GROUP BY `region`
HAVING SUM(`amount`) > 500.00;
```

### Expected Output

```text
+--------+---------------+
| region | total_revenue |
+--------+---------------+
| South  |       1250.00 |
+--------+---------------+
```

## Explanation

1. `region` is the non-aggregated column in `SELECT` and is explicitly listed in `GROUP BY region`, satisfying `ONLY_FULL_GROUP_BY`.
2. `HAVING SUM(amount) > 500.00` filters out regions earning 500.00 or less.
