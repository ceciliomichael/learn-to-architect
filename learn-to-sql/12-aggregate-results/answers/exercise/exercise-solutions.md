# Exercise Solutions: Calculate Aggregate Results

## Exercise 1

```sql
SELECT
  COUNT(*) AS total_books,
  COUNT(published_year) AS known_years,
  COUNT(DISTINCT author) AS distinct_authors
FROM books;
```

The result is 6, 5, and 4.

## Exercise 2

```sql
SELECT
  COUNT(*) AS in_stock_count,
  MIN(price) AS lowest_price,
  MAX(price) AS highest_price,
  round(AVG(price), 2) AS average_price
FROM books
WHERE in_stock = 1;
```

Four rows supply the aggregate inputs.

## Exercise 3

```sql
SELECT
  COUNT(*) AS row_count,
  SUM(price) AS total_price,
  AVG(price) AS average_price
FROM books
WHERE price > 1000;
```

The count is 0. Sum and average are `NULL` because no nonmissing price values exist.
