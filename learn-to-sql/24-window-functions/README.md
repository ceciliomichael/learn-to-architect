# Module 24: Calculate Across Rows with Window Functions

## What you will learn

You will calculate ranks and neighboring values while keeping one output row per input row.

## Windows preserve detail rows

An aggregate with `GROUP BY` collapses rows into summaries. A window function sees related rows but preserves each current row:

```sql
SELECT
  title,
  author,
  price,
  AVG(price) OVER (PARTITION BY author) AS author_average
FROM books
ORDER BY author, title;
```

`OVER` makes the aggregate a window function. `PARTITION BY author` creates an independent calculation group for each author.

## Window ordering defines calculation order

```sql
SELECT
  title,
  price,
  row_number() OVER (ORDER BY price DESC, book_id) AS price_position
FROM books
ORDER BY price_position;
```

The `ORDER BY` inside `OVER` controls row numbering. The final `ORDER BY` controls display. They have different jobs.

The unique `book_id` tie breaker makes numbering deterministic.

## Compare ranking functions

```sql
SELECT
  name,
  price_cents,
  row_number() OVER (ORDER BY price_cents DESC, product_id) AS row_num,
  rank() OVER (ORDER BY price_cents DESC) AS price_rank,
  dense_rank() OVER (ORDER BY price_cents DESC) AS dense_price_rank
FROM products;
```

- `row_number` gives every row a different sequence number.
- `rank` gives peers the same rank and leaves gaps after ties.
- `dense_rank` gives peers the same rank without gaps.

Peers are rows equal on the window's ordering expressions.

## Read previous and next rows

```sql
SELECT
  order_id,
  total_cents,
  lag(total_cents) OVER (ORDER BY order_id) AS previous_total,
  lead(total_cents) OVER (ORDER BY order_id) AS next_total
FROM order_summaries;
```

`lag` and `lead` return a value from a preceding or following row in window order. At an edge, they return `NULL` unless a default argument is supplied.

## Filter window results in an outer query

Window functions are calculated after `WHERE`, grouping, and `HAVING`. They cannot normally appear in `WHERE` at the same query level. Name the result first:

```sql
WITH ranked_books AS (
  SELECT
    book_id,
    title,
    price,
    row_number() OVER (ORDER BY price DESC, book_id) AS position
  FROM books
)
SELECT title, price
FROM ranked_books
WHERE position <= 3
ORDER BY position;
```

## Common mistakes

### Expecting PARTITION BY to group output rows

It divides calculations but preserves rows.

### Omitting tie breakers from row_number

Tied rows can receive positions in an unspecified order.

### Filtering a window alias in the same WHERE

Use a CTE or subquery.

## Check your understanding

You are ready when you can distinguish partitioning, window ordering, and final result ordering.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
