# Exercise Solutions: Update and Delete Rows Safely

## Exercise 1

Choose an existing SKU:

```sql
BEGIN;

SELECT product_id, name, price_cents
FROM products
WHERE sku = 'PEN-BLUE';

UPDATE products
SET price_cents = price_cents + 50
WHERE sku = 'PEN-BLUE';

SELECT changes() AS changed_rows;

SELECT product_id, name, price_cents
FROM products
WHERE sku = 'PEN-BLUE';

ROLLBACK;
```

The changed count should be 1. Repeat the select after rollback to see the old price.

## Exercise 2

Replace 2 with an existing category:

```sql
SELECT product_id, name, active
FROM products
WHERE category_id = 2
  AND active = 1;

BEGIN;

UPDATE products
SET active = 0
WHERE category_id = 2
  AND active = 1;

SELECT changes() AS changed_rows;

SELECT product_id, name, active
FROM products
WHERE category_id = 2;

COMMIT;
```

Commit only if the result matches the preview.

## Exercise 3

Replace the identifier with one inactive practice product:

```sql
SELECT product_id, name, active
FROM products
WHERE product_id = 2
  AND active = 0;

BEGIN;

DELETE FROM products
WHERE product_id = 2
  AND active = 0;

SELECT changes() AS changed_rows;

SELECT * FROM products
WHERE product_id = 2;

ROLLBACK;
```

Use only an identifier that your preview proves is safe. After rollback, the row should exist again.
