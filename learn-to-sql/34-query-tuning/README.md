# Module 34: Tune Queries with Evidence

## What you will learn

You will define a workload, measure plans and execution, change one cause, and prove whether the result improved.

## Performance is a measured requirement

Start with a statement such as:

```text
The product search must return its first 50 rows within 100 ms at the 95th percentile with 2 million products and 40 concurrent sessions.
```

Without data volume, distribution, concurrency, result size, and latency target, fast is not testable.

## Reduce unnecessary work first

Check:

- Are only needed columns selected?
- Are filters correct and selective?
- Does a join multiply rows accidentally?
- Is sorting required and deterministic?
- Can pagination avoid a large offset?
- Is the application issuing one query per row instead of one set query?

Correct query shape often matters more than adding an index.

## SQLite evidence

```sql
EXPLAIN QUERY PLAN
SELECT product_id, name
FROM products
WHERE category_id = 2 AND active = 1
ORDER BY price_cents
LIMIT 50;
```

Compare before and after a candidate index with representative data. Time the actual query in the intended application path. Plan output is high-level and version-dependent.

## PostgreSQL EXPLAIN

```sql
EXPLAIN
SELECT product_id, name
FROM app.products
WHERE category_id = 2 AND active = true;
```

Plain `EXPLAIN` shows the chosen plan and estimates without executing the query.

```sql
EXPLAIN (ANALYZE, BUFFERS)
SELECT product_id, name
FROM app.products
WHERE category_id = 2 AND active = true;
```

`ANALYZE` executes the statement and reports actual timing and row counts. Do not use it carelessly on insert, update, delete, expensive production queries, or lock-heavy statements. Test safely and remember that cache state affects timing.

Compare estimated rows with actual rows. Large differences can point to stale statistics, correlated columns, skewed values, or expressions the planner cannot estimate well.

## Selectivity and indexes

Selectivity describes how much a condition narrows rows. An index on a nearly unique email can be valuable. An index on a boolean alone often matches a large portion of the table and may not beat a scan.

Composite, partial, expression, and covering indexes should match repeated important query shapes. Every additional index increases storage and write cost.

## Keep columns usable by indexes

A condition that wraps a column may not use a plain index:

```sql
WHERE lower(email) = lower($1)
```

A suitable expression index can help if the exact expression and collation rules match. Alternatively, store and validate a canonical form when the domain permits it. Do not rewrite conditions only for speed if meaning changes.

## Update statistics and maintain health

SQLite uses `ANALYZE` and `PRAGMA optimize`. PostgreSQL uses `ANALYZE` and normally relies on autovacuum to maintain statistics and reclaim reusable space. Tune maintenance only from monitoring and official guidance.

## A repeatable tuning loop

1. Capture the exact slow statement and parameters.
2. Reproduce representative data and concurrency.
3. Record baseline latency, rows, plan, and resource use.
4. Identify one likely cause.
5. Make one focused change.
6. Measure reads and writes again.
7. Test correctness and edge cases.
8. Keep, revise, or revert from evidence.
9. Add a performance regression check where stable.

## Common mistakes

### Comparing warm and cold runs as equals

Record cache and environment conditions.

### Trusting estimated cost across different systems

Planner cost is an internal comparison unit, not elapsed milliseconds.

### Improving one query while harming writes

Measure the whole important workload.

## Check your understanding

You are ready when you can form a measurable target, read estimated versus actual rows, and justify an index from workload evidence.
