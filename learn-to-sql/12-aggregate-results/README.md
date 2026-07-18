# Module 12: Calculate Aggregate Results

## What you will learn

You will summarize several input rows as one result using count, sum, average, minimum, and maximum.

## Aggregates consume a set of rows

```sql
SELECT COUNT(*) AS product_count
FROM products;
```

`COUNT(*)` counts result rows, including rows that contain `NULL` in some columns.

```sql
SELECT COUNT(published_year) AS known_year_count
FROM books;
```

`COUNT(column)` counts only rows where that expression is not `NULL`. In `library.db`, it returns 5 while `COUNT(*)` returns 6.

## Summarize numbers

```sql
SELECT
  SUM(price_cents) AS total_price_cents,
  AVG(price_cents) AS average_price_cents,
  MIN(price_cents) AS lowest_price_cents,
  MAX(price_cents) AS highest_price_cents
FROM products;
```

These functions ignore `NULL` inputs. If no nonmissing value exists, `SUM`, `AVG`, `MIN`, and `MAX` normally return `NULL`. `COUNT` returns zero for an empty input set.

## Filter before aggregating

```sql
SELECT COUNT(*) AS active_product_count
FROM products
WHERE active = 1;
```

`WHERE` chooses input rows before the aggregate runs.

```sql
SELECT AVG(price_cents) AS active_average
FROM products
WHERE active = 1;
```

## Count distinct known values

```sql
SELECT COUNT(DISTINCT category_id) AS used_categories
FROM products;
```

This counts distinct non-`NULL` category identifiers. SQLite supports one expression inside this form. Product syntax can differ for distinct combinations.

## Do not mix detail and summary accidentally

This request is incomplete in standard relational reasoning:

```sql
SELECT name, AVG(price_cents)
FROM products;
```

Which one product name should represent the average of all products? SQLite may return an arbitrary bare value in some aggregate queries, but other databases reject it. Select only aggregated expressions until `GROUP BY` gives each detail column a clear group meaning.

## Common mistakes

### Using COUNT(column) when missing rows should count

Use `COUNT(*)` for rows.

### Replacing an empty average with zero automatically

No known inputs is different from an average of zero. Apply a fallback only if the domain defines it.

### Selecting a nonaggregated column without grouping

SQLite's permissive result can hide an ill-defined question. Write portable, meaningful queries.

## Check your understanding

You are ready when you can choose between `COUNT(*)` and `COUNT(column)` and predict how `NULL` affects each aggregate.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
