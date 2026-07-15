# Exercise Solutions: Filter Rows with Comparisons

## Exercise 1

```sql
SELECT title, price
FROM books
WHERE price >= 30;

SELECT title, author
FROM books
WHERE author = 'Lena Ortiz';

SELECT title, in_stock
FROM books
WHERE in_stock = 0;
```

The first returns Quiet Algorithms and Type Safe Programs. The second returns Web Basics and Type Safe Programs. The third returns Quiet Algorithms and Data Stories.

## Exercise 2

```sql
SELECT title, price, in_stock
FROM books
WHERE in_stock = 1
  AND price < 30;

SELECT title, author
FROM books
WHERE author = 'Mira Chen'
   OR author = 'Lena Ortiz';

SELECT title, author, price
FROM books
WHERE (author = 'Mira Chen' OR author = 'Lena Ortiz')
  AND price >= 25;
```

The final query returns Practical Databases and Type Safe Programs. Web Basics fails the price condition, and First Steps in SQL also costs less than 25.

## Exercise 3

```sql
SELECT title, price
FROM books
WHERE price BETWEEN 20 AND 30;

SELECT title, published_year
FROM books
WHERE published_year IN (2019, 2021, 2023);

SELECT title
FROM books
WHERE title LIKE 'P%';

SELECT title
FROM books
WHERE title LIKE '%Safe%';
```

`P%` finds Practical Databases. `%Safe%` finds Type Safe Programs.
