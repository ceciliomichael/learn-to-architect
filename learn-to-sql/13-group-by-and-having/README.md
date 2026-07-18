# Module 13: Group Rows and Filter Groups

## What you will learn

You will form groups, calculate one summary per group, and filter after aggregation.

## GROUP BY creates one result per group

```sql
SELECT
  author,
  COUNT(*) AS book_count
FROM books
GROUP BY author
ORDER BY author;
```

Rows with the same author value form one group. `COUNT(*)` runs separately for each group.

Every selected detail expression should be a grouping expression or be functionally determined by it in a way the target database accepts. The clearest portable starting rule is: select grouping columns and aggregate expressions only.

## Group by several values

```sql
SELECT
  author,
  in_stock,
  COUNT(*) AS book_count
FROM books
GROUP BY author, in_stock
ORDER BY author, in_stock;
```

Each distinct author and stock combination becomes a group.

## WHERE filters rows before grouping

```sql
SELECT author, AVG(price) AS average_price
FROM books
WHERE in_stock = 1
GROUP BY author;
```

Out-of-stock rows never enter a group.

## HAVING filters groups after aggregation

```sql
SELECT
  author,
  COUNT(*) AS book_count
FROM books
GROUP BY author
HAVING COUNT(*) >= 2
ORDER BY author;
```

`HAVING` can use aggregate conditions because it is evaluated after groups exist. Use `WHERE` for ordinary row conditions so fewer rows need grouping and the intention remains clear.

## NULL forms a group

All `NULL` grouping values belong to one group for grouping purposes, even though ordinary equality with `NULL` is unknown. Label it for display when needed:

```sql
SELECT
  COALESCE(published_year, 'Unknown') AS year_label,
  COUNT(*) AS book_count
FROM books
GROUP BY published_year
ORDER BY published_year IS NULL, published_year;
```

## Avoid SQLite bare-column shortcuts

SQLite permits some selected columns that are neither grouped nor aggregated. Their values may not represent the group meaningfully. PostgreSQL usually rejects such queries unless a valid dependency is recognized. Write the clear portable form instead of relying on a convenient accident.

## Common mistakes

### Using WHERE with COUNT

`WHERE COUNT(*) > 1` is invalid because groups do not exist yet. Use `HAVING`.

### Grouping by too many columns

Every extra grouping expression divides groups further. Match the requested result grain.

### Selecting an arbitrary group member

Aggregate it or add a real grouping reason.

## Check your understanding

You are ready when you can state the result grain, place row filters in `WHERE`, and place aggregate filters in `HAVING`.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
