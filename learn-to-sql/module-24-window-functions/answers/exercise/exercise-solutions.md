# Exercise Solutions: Calculate Across Rows with Window Functions

## Exercise 1

```sql
SELECT title, author, price,
       round(AVG(price) OVER (PARTITION BY author), 2) AS author_average
FROM books
ORDER BY author, title;
```

## Exercise 2

```sql
SELECT title, price,
       row_number() OVER (ORDER BY price DESC, book_id) AS row_num,
       rank() OVER (ORDER BY price DESC) AS price_rank,
       dense_rank() OVER (ORDER BY price DESC) AS dense_rank
FROM books
ORDER BY price DESC, book_id;
```

Tied prices share rank values. Rank leaves a gap; dense rank does not. Row number remains unique.

## Exercise 3

```sql
WITH ranked AS (
  SELECT title, author, price,
         row_number() OVER (
           PARTITION BY author
           ORDER BY price DESC, book_id
         ) AS author_position
  FROM books
)
SELECT title, author, price
FROM ranked
WHERE author_position = 1
ORDER BY author;
```
