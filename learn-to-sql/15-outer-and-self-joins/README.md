# Module 15: Keep Unmatched Rows with Outer Joins

## What you will learn

You will keep rows without matches, place filters correctly, and join a table to itself.

## LEFT JOIN preserves its left input

```sql
SELECT
  c.category_id,
  c.name AS category_name,
  p.name AS product_name
FROM categories AS c
LEFT JOIN products AS p
  ON p.category_id = c.category_id
ORDER BY c.category_id, p.product_id;
```

Every category appears. If no product matches, product columns are `NULL`. A category with several products appears several times because the result grain is one row per category-product match, plus one missing-match row for empty categories.

## Find parents with no children

```sql
SELECT c.category_id, c.name
FROM categories AS c
LEFT JOIN products AS p
  ON p.category_id = c.category_id
WHERE p.product_id IS NULL;
```

The child primary key can only be `NULL` in the result when no child row matched.

## Filter placement changes outer joins

Keep all categories but join only active products:

```sql
SELECT c.name, p.name
FROM categories AS c
LEFT JOIN products AS p
  ON p.category_id = c.category_id
 AND p.active = 1;
```

Putting `p.active = 1` in `WHERE` removes missing-match rows because their value is `NULL`, making the result behave like an inner join for that condition.

Use `ON` when the condition decides which right-side rows count as matches. Use `WHERE` when the completed result row must satisfy the condition.

## Join a table to itself

An employee can refer to another employee as manager:

```sql
CREATE TABLE employees (
  employee_id INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  manager_id INTEGER,
  FOREIGN KEY (manager_id) REFERENCES employees(employee_id)
) STRICT;
```

Read employees and optional managers:

```sql
SELECT
  e.name AS employee_name,
  m.name AS manager_name
FROM employees AS e
LEFT JOIN employees AS m
  ON m.employee_id = e.manager_id;
```

Aliases give the same table two roles.

## RIGHT and FULL joins

Current SQLite versions support `RIGHT JOIN` and `FULL JOIN`, but many older SQLite deployments do not. `LEFT JOIN` remains the most portable outer join. PostgreSQL supports left, right, and full outer joins. Check the deployed product and version.

## Common mistakes

### Filtering right-side rows in WHERE unintentionally

This can discard the unmatched left rows you meant to preserve.

### Counting rows instead of nonmissing children

After a left join, `COUNT(*)` counts the preserved unmatched row. Use `COUNT(p.product_id)` to count actual products.

### Joining a self-reference without aliases

Use role names such as `e` and `m` so every column source is clear.

## Check your understanding

You are ready when you can predict unmatched rows and explain why moving a predicate between `ON` and `WHERE` can change the result.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
