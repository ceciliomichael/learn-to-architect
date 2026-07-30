# Module 08 Exercise Solution

```sql
SELECT 
  region, 
  COUNT(*) AS total_transactions, 
  AVG(amount) AS avg_sale 
FROM sales 
GROUP BY region 
HAVING AVG(amount) >= 120.00;
```

### Expected Output

```text
┌────────┬────────────────────┬──────────┐
│ region │ total_transactions │ avg_sale │
├────────┼────────────────────┼──────────┤
│ North  │ 2                  │ 125.0    │
│ South  │ 2                  │ 250.0    │
└────────┴────────────────────┴──────────┘
```

## Explanation

1. `GROUP BY region` clusters rows into North, South, East buckets.
2. `HAVING AVG(amount) >= 120.00` excludes East (which has avg 50.0).
