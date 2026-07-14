# Exercise Solutions: Sort, Remove Duplicates, and Limit Results

## Exercise 1

```sql
SELECT title, published_year
FROM books
ORDER BY published_year IS NULL, published_year DESC, book_id;

SELECT title, author
FROM books
ORDER BY author, title, book_id;
```

The first condition places known values before the missing one, then sorts known years newest first.

## Exercise 2

```sql
SELECT DISTINCT author
FROM books
ORDER BY author;

SELECT DISTINCT author, in_stock
FROM books
ORDER BY author, in_stock;
```

Distinct compares the whole selected row. One author can have both a 0 and 1 stock combination.

## Exercise 3

```sql
SELECT title, price
FROM books
ORDER BY price ASC, book_id ASC
LIMIT 2;

SELECT title, price
FROM books
ORDER BY price ASC, book_id ASC
LIMIT 2 OFFSET 2;
```

The common deterministic order makes the second request continue the same ordered sequence.
