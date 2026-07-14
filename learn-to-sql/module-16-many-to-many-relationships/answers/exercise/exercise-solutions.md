# Exercise Solutions: Model Many-to-Many Relationships

## Exercise 1

After creating the tables, inspect available products and use their real identifiers:

```sql
INSERT INTO orders (customer_name, status)
VALUES ('Ava Cruz', 'paid'), ('Noah Lim', 'open');

INSERT INTO order_items
  (order_id, product_id, quantity, unit_price_cents)
VALUES
  (1, 1, 2, 2500),
  (1, 2, 1, 1200),
  (2, 2, 3, 1200);
```

Adjust product identifiers and prices to existing rows in your database.

## Exercise 2

```sql
SELECT
  o.order_id,
  o.customer_name,
  p.name,
  oi.quantity,
  oi.unit_price_cents,
  oi.quantity * oi.unit_price_cents AS line_total_cents
FROM orders AS o
JOIN order_items AS oi ON oi.order_id = o.order_id
JOIN products AS p ON p.product_id = oi.product_id
ORDER BY o.order_id, p.name;

SELECT
  o.order_id,
  o.customer_name,
  SUM(oi.quantity * oi.unit_price_cents) AS total_cents
FROM orders AS o
JOIN order_items AS oi ON oi.order_id = o.order_id
GROUP BY o.order_id, o.customer_name
ORDER BY o.order_id;
```

## Exercise 3

Repeat an existing `(order_id, product_id)` pair. The composite primary key rejects it. Find unused products with:

```sql
SELECT p.product_id, p.name
FROM products AS p
LEFT JOIN order_items AS oi
  ON oi.product_id = p.product_id
WHERE oi.order_id IS NULL;
```
