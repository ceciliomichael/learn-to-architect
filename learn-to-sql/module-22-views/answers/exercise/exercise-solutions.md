# Exercise Solutions: Create and Use Views

## Exercise 1

```sql
CREATE VIEW order_summaries AS
SELECT
  o.order_id,
  o.customer_name,
  o.status,
  SUM(oi.quantity * oi.unit_price_cents) AS total_cents
FROM orders AS o
JOIN order_items AS oi ON oi.order_id = o.order_id
GROUP BY o.order_id, o.customer_name, o.status;

SELECT * FROM order_summaries ORDER BY order_id;
```

## Exercise 2

Use an existing order and a product not yet in that order:

```sql
BEGIN;
INSERT INTO order_items (order_id, product_id, quantity, unit_price_cents)
VALUES (1, 3, 1, 500);
SELECT * FROM order_summaries WHERE order_id = 1;
ROLLBACK;
SELECT * FROM order_summaries WHERE order_id = 1;
```

Adjust identifiers and price so constraints are satisfied. The view reflects base tables at query time.

## Exercise 3

```text
.schema order_summaries
.tables
```

```sql
DROP VIEW order_summaries;
SELECT COUNT(*) FROM orders;
```

Orders remain because only the view definition was removed.
