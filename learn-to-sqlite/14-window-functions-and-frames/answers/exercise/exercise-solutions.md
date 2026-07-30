# Module 14 Exercise Solution

```sql
WITH ranked_employees AS (
  SELECT 
    name, 
    department, 
    salary,
    ROW_NUMBER() OVER(PARTITION BY department ORDER BY salary DESC) AS rn
  FROM employees
)
SELECT name, department, salary
FROM ranked_employees
WHERE rn = 1;
```

### Expected Output

```text
┌───────┬─────────────┬─────────┐
│ name  │ department  │ salary  │
├───────┼─────────────┼─────────┤
│ Alice │ Engineering │ 95000.0 │
│ Bob   │ Marketing   │ 82000.0 │
└───────┴─────────────┴─────────┘
```

## Explanation

1. `ROW_NUMBER() OVER(PARTITION BY department ORDER BY salary DESC)` assigns rank 1 to the highest earner in each department.
2. The CTE allows `WHERE rn = 1` filtering (since window functions cannot be directly used in `WHERE`).
