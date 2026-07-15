# Exercise Solutions: Walk Hierarchies with Recursive CTEs

## Exercise 1

```sql
INSERT INTO employees (employee_id, name, manager_id) VALUES
  (1, 'Ava', NULL), (2, 'Ben', 1), (3, 'Cleo', 1),
  (4, 'Dina', 2), (5, 'Eli', 3);

WITH RECURSIVE organization AS (
  SELECT employee_id, name, manager_id, 0 AS depth
  FROM employees WHERE manager_id IS NULL
  UNION ALL
  SELECT e.employee_id, e.name, e.manager_id, o.depth + 1
  FROM employees AS e
  JOIN organization AS o ON e.manager_id = o.employee_id
)
SELECT * FROM organization ORDER BY depth, employee_id;
```

## Exercise 2

```sql
WITH RECURSIVE subtree AS (
  SELECT employee_id, name, manager_id, name AS path
  FROM employees WHERE employee_id = 2
  UNION ALL
  SELECT e.employee_id, e.name, e.manager_id,
         subtree.path || ' > ' || e.name
  FROM employees AS e
  JOIN subtree ON e.manager_id = subtree.employee_id
)
SELECT * FROM subtree ORDER BY path;
```

## Exercise 3

Rows A with manager B and B with manager A satisfy existence checks. A write-time cycle check must walk proposed ancestors before accepting the change. A read-time visited path refuses an identifier already seen and prevents revisiting the cycle.
