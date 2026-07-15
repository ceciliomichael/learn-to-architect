# Exercise Solutions: Understand NULL and Three-Valued Logic

## Exercise 1

```sql
SELECT title, published_year
FROM books
WHERE published_year IS NULL;

SELECT title, published_year
FROM books
WHERE published_year IS NOT NULL;
```

The first returns one row, Web Basics. The second returns five rows.

## Exercise 2

```sql
SELECT title, published_year
FROM books
WHERE published_year <> 2024;

SELECT title, published_year
FROM books
WHERE published_year <> 2024
   OR published_year IS NULL;
```

The first returns four known non-2024 years. The second returns five rows because it deliberately includes Web Basics.

## Exercise 3

```sql
SELECT
  title,
  COALESCE(published_year, 'Not recorded') AS year_display
FROM books;

SELECT title, published_year
FROM books
WHERE title = 'Web Basics'
  AND published_year IS NULL;
```

The second query still finds the row. `COALESCE` only shaped the earlier result.
