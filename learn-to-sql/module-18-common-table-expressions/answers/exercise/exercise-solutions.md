# Exercise Solutions: Organize Queries with Common Table Expressions

## Exercise 1

```sql
WITH affordable_books AS (
  SELECT book_id, title, price
  FROM books
  WHERE price < 25
)
SELECT title, price
FROM affordable_books
ORDER BY price, book_id;
```

## Exercise 2

```sql
WITH
order_totals AS (
  SELECT
    o.order_id,
    o.customer_name,
    SUM(oi.quantity * oi.unit_price_cents) AS total_cents
  FROM orders AS o
  JOIN order_items AS oi ON oi.order_id = o.order_id
  GROUP BY o.order_id, o.customer_name
),
large_orders AS (
  SELECT order_id, customer_name, total_cents
  FROM order_totals
  WHERE total_cents >= 2000
)
SELECT order_id, customer_name, total_cents
FROM large_orders
ORDER BY total_cents DESC, order_id;
```

## Exercise 3

`order_totals` has one row per order. `large_orders` has one row per qualifying order. The final result keeps that same one-row-per-order grain.
