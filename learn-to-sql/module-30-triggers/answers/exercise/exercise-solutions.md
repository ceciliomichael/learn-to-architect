# Exercise Solutions: Use Triggers Carefully

## Exercise 1

Run the exact table and trigger statements from the lesson, then:

```sql
BEGIN;
UPDATE products SET price_cents = price_cents + 25 WHERE product_id = 1;
SELECT * FROM products WHERE product_id = 1;
SELECT * FROM product_price_audit ORDER BY audit_id DESC LIMIT 1;
```

The audit should show old and new prices.

## Exercise 2

```sql
ROLLBACK;
SELECT * FROM product_price_audit;

BEGIN;
UPDATE products
SET price_cents = price_cents
WHERE product_id = 1;
SELECT changes() AS product_rows_matched;
SELECT COUNT(*) AS audit_count FROM product_price_audit;
COMMIT;
```

The update can report a matched row, but the trigger `WHEN` prevents an audit insert because the price is unchanged.

## Exercise 3

One correct contract is: after a product price update, when old and new prices differ, insert one UTC-stamped row into `product_price_audit`. A failed audit insert fails the outer statement. Remove with `DROP TRIGGER products_price_audit;` during a reviewed migration.
