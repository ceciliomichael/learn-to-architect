# Exercise Solutions: Join Matching Rows

## Exercise 1

```sql
SELECT
  p.product_id,
  p.name AS product_name,
  c.name AS category_name,
  p.price_cents
FROM products AS p
INNER JOIN categories AS c
  ON c.category_id = p.category_id
ORDER BY p.product_id;
```

## Exercise 2

```sql
SELECT p.name, c.name AS category_name, p.price_cents
FROM products AS p
INNER JOIN categories AS c
  ON c.category_id = p.category_id
WHERE p.active = 1
  AND c.name = 'Books'
ORDER BY p.name;
```

Choose another existing category if needed.

## Exercise 3

```sql
SELECT COUNT(*) FROM products;
SELECT COUNT(*) FROM categories;

SELECT COUNT(*) AS combination_count
FROM products AS p
CROSS JOIN categories AS c;

SELECT COUNT(*) AS matched_count
FROM products AS p
JOIN categories AS c
  ON c.category_id = p.category_id;
```

The cross count is product count times category count. The proper join normally has one matched row per product.
