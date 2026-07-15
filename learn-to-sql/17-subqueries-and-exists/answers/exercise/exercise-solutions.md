# Exercise Solutions: Use Subqueries and EXISTS

## Exercise 1

```sql
SELECT AVG(price) AS overall_average FROM books;

SELECT title, price
FROM books
WHERE price < (SELECT AVG(price) FROM books)
ORDER BY price, book_id;
```

`AVG` without grouping returns one row and one column.

## Exercise 2

```sql
SELECT c.category_id, c.name
FROM categories AS c
WHERE EXISTS (
  SELECT 1 FROM products AS p
  WHERE p.category_id = c.category_id
);

SELECT c.category_id, c.name
FROM categories AS c
WHERE NOT EXISTS (
  SELECT 1 FROM products AS p
  WHERE p.category_id = c.category_id
);
```

## Exercise 3

```sql
SELECT product_id, name
FROM products
WHERE category_id IN (
  SELECT category_id
  FROM categories
  WHERE name LIKE 'B%' OR name LIKE 'S%'
);

SELECT p.product_id, p.name
FROM products AS p
JOIN categories AS c ON c.category_id = p.category_id
WHERE c.name LIKE 'B%' OR c.name LIKE 'S%';
```

Both express the same membership for this schema.
