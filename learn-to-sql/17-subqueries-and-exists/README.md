# Module 17: Use Subqueries and EXISTS

## What you will learn

You will use one query's result inside another and choose between scalar, membership, and existence questions.

## A scalar subquery returns one value

Find books priced above the average:

```sql
SELECT title, price
FROM books
WHERE price > (
  SELECT AVG(price)
  FROM books
)
ORDER BY price;
```

The inner query returns one average value. The outer query compares each price with it. A scalar subquery should return one row and one column. No rows becomes `NULL`; several rows cause an error in many products, while SQLite may take the first row. Write the query so one value is guaranteed.

## IN tests membership in one-column results

```sql
SELECT name
FROM products
WHERE category_id IN (
  SELECT category_id
  FROM categories
  WHERE name IN ('Books', 'Stationery')
);
```

The inner result must have one column. The outer condition tests whether each category identifier is in that set.

## EXISTS asks whether any row exists

```sql
SELECT c.category_id, c.name
FROM categories AS c
WHERE EXISTS (
  SELECT 1
  FROM products AS p
  WHERE p.category_id = c.category_id
);
```

This is correlated: the inner query refers to the current outer category. `EXISTS` becomes true as soon as a matching row exists. The selected `1` is a convention because the actual inner columns are irrelevant.

Find parents without children:

```sql
SELECT c.category_id, c.name
FROM categories AS c
WHERE NOT EXISTS (
  SELECT 1
  FROM products AS p
  WHERE p.category_id = c.category_id
);
```

## Beware NOT IN with NULL

If a `NOT IN` subquery returns even one `NULL`, comparisons can become unknown and no outer row may pass:

```sql
value NOT IN (1, 2, NULL)
```

Use a declared nonmissing key or prefer correlated `NOT EXISTS` for anti-relationship questions.

## A subquery in FROM is a result source

```sql
SELECT price_band, COUNT(*) AS book_count
FROM (
  SELECT
    CASE WHEN price < 25 THEN 'lower' ELSE 'higher' END AS price_band
  FROM books
) AS classified_books
GROUP BY price_band;
```

The derived table needs an alias. Module 18 gives the inner result a name above the main query, which is often easier to read.

## Common mistakes

### Returning several columns to IN

The simple membership form expects one comparable column.

### Using NOT IN with a nullable result

Unknown logic can empty the result. Use `NOT EXISTS`.

### Using a subquery when a join states the relationship better

Choose the form that makes grain and purpose clearest, then verify its plan when performance matters.

## Check your understanding

You are ready when you can identify the shape required from an inner query and choose `EXISTS` for a yes-or-no relationship question.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
