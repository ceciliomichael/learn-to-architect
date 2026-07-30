# Module 10 Exercise Solution

```sql
WITH avg_dept_salaries AS (
  SELECT dept_id, AVG(salary) AS avg_sal
  FROM employees
  GROUP BY dept_id
)
SELECT d.name, ads.avg_sal
FROM avg_dept_salaries ads
JOIN departments d ON ads.dept_id = d.dept_id;
```

### Expected Output

```text
┌─────────────┬─────────┐
│    name     │ avg_sal │
├─────────────┼─────────┤
│ Engineering │ 95000.0 │
│ Marketing   │ 82000.0 │
└─────────────┴─────────┘
```

## Explanation

1. `WITH avg_dept_salaries AS (...)` isolates the aggregation phase.
2. The outer `SELECT` joins the CTE with `departments` for readable output.
