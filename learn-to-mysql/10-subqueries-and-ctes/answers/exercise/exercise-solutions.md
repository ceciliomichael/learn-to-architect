# Module 10 Exercise Solution

```sql
WITH `high_earners` AS (
  SELECT `name`, `dept_id`, `salary`
  FROM `employees`
  WHERE `salary` > 80000.00
)
SELECT d.`name` AS `department`, he.`name` AS `employee`, he.`salary`
FROM `high_earners` he
JOIN `departments` d ON he.`dept_id` = d.`dept_id`;
```

### Expected Output

```text
+-------------+----------+----------+
| department  | employee | salary   |
+-------------+----------+----------+
| Engineering | Alice    | 95000.00 |
| Marketing   | Bob      | 82000.00 |
+-------------+----------+----------+
```

## Explanation

1. The `WITH high_earners AS (...)` CTE filters high earners first.
2. The outer query joins the CTE with `departments` for readable output.
