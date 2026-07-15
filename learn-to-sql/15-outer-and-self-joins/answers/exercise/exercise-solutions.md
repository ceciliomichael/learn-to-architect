# Exercise Solutions: Keep Unmatched Rows with Outer Joins

## Exercise 1

```sql
INSERT INTO categories (name)
VALUES ('Empty Practice Category');

SELECT c.name AS category_name, p.name AS product_name
FROM categories AS c
LEFT JOIN products AS p
  ON p.category_id = c.category_id
ORDER BY c.name, p.name;
```

The practice category appears once with `NULL` for product name.

## Exercise 2

```sql
SELECT
  c.category_id,
  c.name,
  COUNT(p.product_id) AS product_count
FROM categories AS c
LEFT JOIN products AS p
  ON p.category_id = c.category_id
GROUP BY c.category_id, c.name
ORDER BY c.category_id;
```

The empty category count is zero because `COUNT` ignores its missing child identifier.

## Exercise 3

```sql
SELECT c.name, p.name
FROM categories AS c
LEFT JOIN products AS p
  ON p.category_id = c.category_id
 AND p.active = 1;

SELECT c.name, p.name
FROM categories AS c
LEFT JOIN products AS p
  ON p.category_id = c.category_id
WHERE p.active = 1;
```

The first preserves every category. The second removes rows with no active match because `NULL = 1` is unknown.
