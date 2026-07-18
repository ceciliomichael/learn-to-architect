# Module 23: Create Indexes and Read Query Plans

## What you will learn

You will create evidence-based indexes and use SQLite's high-level plan output without overreading it.

## An index is an additional search structure

```sql
CREATE INDEX products_category_idx
ON products (category_id);
```

SQLite B-tree indexes store ordered key values and row locators. They can reduce rows examined for matching and ordering. They also use disk space and add work to inserts, updates, and deletes.

Primary and unique constraints already create needed uniqueness structures. Do not duplicate them without evidence.

## Inspect a high-level plan

```sql
EXPLAIN QUERY PLAN
SELECT product_id, name
FROM products
WHERE category_id = 2;
```

Look for broad evidence such as a table scan or a search using an index. SQLite explicitly warns that `EXPLAIN QUERY PLAN` output format can change between releases. Use it for interactive analysis, not application logic or brittle text tests.

## Composite index order matters

```sql
CREATE INDEX products_category_active_price_idx
ON products (category_id, active, price_cents);
```

This can help queries starting with equality conditions on category and active, then using price for range or order. It is not equally useful for every query on price alone. Think from the leftmost index columns and the actual predicates.

One composite index may make a shorter prefix index unnecessary, but confirm with workload and plans before removing anything.

## Cover a query carefully

If all required values are available from an index, SQLite may report a covering index and avoid reading the table for those rows. Adding every selected column to chase covering behavior can create large costly indexes. Measure the tradeoff.

## Partial and expression indexes

SQLite supports focused indexes:

```sql
CREATE INDEX active_products_price_idx
ON products (price_cents)
WHERE active = 1;

CREATE INDEX products_lower_name_idx
ON products (lower(name));
```

The query predicate or expression must match in a way the planner recognizes. Expression functions used in indexes must meet SQLite rules, including determinism.

## Statistics help the planner

```sql
ANALYZE;
```

Statistics help estimate selectivity. Current SQLite versions also offer `PRAGMA optimize`, which can run appropriate analysis efficiently:

```sql
PRAGMA optimize;
```

Follow the deployed SQLite documentation and application lifecycle. A tiny course table may choose a scan because it is genuinely cheaper.

## Remove an unused index

```sql
DROP INDEX products_category_idx;
```

Do this only after measuring representative reads and writes and checking that no required uniqueness depends on it.

## Common mistakes

### Adding one index per column

Indexes should serve real query shapes, not column inventory.

### Expecting an index always to be used

The planner chooses estimated cost. A scan can be correct for small or unselective data.

### Testing only a tiny dataset

Use representative volume and value distribution before production decisions.

## Check your understanding

You are ready when you can connect an index column order to a query and explain its read, write, and storage tradeoffs.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
