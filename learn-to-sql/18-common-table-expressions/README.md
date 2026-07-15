# Module 18: Organize Queries with Common Table Expressions

## What you will learn

You will name intermediate query results with `WITH` and build larger requests as understandable steps.

## Name a result before the main query

```sql
WITH active_products AS (
  SELECT product_id, category_id, name, price_cents
  FROM products
  WHERE active = 1
)
SELECT name, price_cents
FROM active_products
ORDER BY price_cents DESC;
```

`active_products` exists only for this statement. It is not a stored table.

## Use several named steps

```sql
WITH
category_totals AS (
  SELECT category_id, COUNT(*) AS product_count
  FROM products
  GROUP BY category_id
),
large_categories AS (
  SELECT category_id, product_count
  FROM category_totals
  WHERE product_count >= 2
)
SELECT c.name, l.product_count
FROM large_categories AS l
JOIN categories AS c
  ON c.category_id = l.category_id
ORDER BY c.name;
```

Later CTEs can refer to earlier ones. Give each name a meaning, not a step number.

## CTE compared with a subquery

Both can express the same logic. A CTE helps when:

- The intermediate result has a useful name
- The main query would otherwise contain deep nesting
- The result is referenced more than once
- You want to inspect each step separately while developing

A CTE is not automatically faster. SQLite may inline or materialize it depending on the query and supported hints. Let clarity lead, then inspect the plan.

## Keep one clear grain per step

Write a comment or sentence before coding:

```text
category_totals has one row per category_id
```

Then ensure every selected expression matches that grain. This makes joins between steps predictable.

## CTE scope and names

The names exist for the single statement. They can shadow table names, so choose names that do not confuse readers. The final statement may be `SELECT`, `INSERT`, `UPDATE`, or `DELETE` in SQLite where syntax permits, but begin with read-only composition.

Recursive CTEs use the same `WITH` idea plus a self-reference and are taught in Module 27.

## Common mistakes

### Ending the CTE before its main statement

Do not put a semicolon between the closing CTE parenthesis and the final query.

### Hiding unclear logic behind many names

Each CTE should have a clear purpose and grain.

### Assuming CTE means cached result

Execution strategy is a planner decision. Inspect rather than assume.

## Check your understanding

You are ready when you can turn a nested query into named steps and state the row grain of each CTE.
