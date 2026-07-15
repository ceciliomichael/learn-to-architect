# Exercise Solutions: Group Rows and Filter Groups

## Exercise 1

```sql
SELECT
  author,
  COUNT(*) AS book_count,
  MIN(price) AS lowest_price,
  MAX(price) AS highest_price,
  round(AVG(price), 2) AS average_price
FROM books
GROUP BY author
ORDER BY author;
```

## Exercise 2

```sql
SELECT
  author,
  round(AVG(price), 2) AS average_price
FROM books
WHERE in_stock = 1
GROUP BY author
HAVING AVG(price) >= 25
ORDER BY author;
```

`WHERE` excludes out-of-stock source rows. `HAVING` excludes completed author groups whose average is too low.

## Exercise 3

```sql
SELECT author, in_stock, COUNT(*) AS book_count
FROM books
GROUP BY author, in_stock
ORDER BY author, in_stock;
```

Lena Ortiz creates one group because both of her books are in stock. Mira Chen also creates one. Authors with one book create one each.
