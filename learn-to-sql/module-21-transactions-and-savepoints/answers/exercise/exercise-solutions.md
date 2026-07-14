# Exercise Solutions: Use Transactions and Savepoints

## Exercise 1

```sql
BEGIN;
SELECT product_id, price_cents FROM products WHERE product_id IN (1, 2);
UPDATE products SET price_cents = price_cents + 100 WHERE product_id IN (1, 2);
SELECT changes(), product_id, price_cents FROM products WHERE product_id IN (1, 2);
ROLLBACK;
SELECT product_id, price_cents FROM products WHERE product_id IN (1, 2);
```

Use identifiers present in your database. The final values should match the first result.

## Exercise 2

```sql
BEGIN;
INSERT INTO orders (order_id, customer_name, status)
VALUES (10001, 'Practice Buyer', 'open');
```

Use existing product identifiers:

```sql
INSERT INTO order_items (order_id, product_id, quantity, unit_price_cents)
VALUES (10001, 1, 1, 2500), (10001, 2, 2, 1200);

SELECT SUM(quantity * unit_price_cents) AS total_cents
FROM order_items
WHERE order_id = 10001;

COMMIT;
```

If product identifiers 1 and 2 do not exist in your practice database, select two existing products and use their identifiers and prices. The explicit order identifier keeps this solution internally consistent.

## Exercise 3

```sql
BEGIN;
UPDATE orders SET status = 'paid' WHERE order_id = 1;
SAVEPOINT quantity_test;
UPDATE order_items SET quantity = quantity + 10 WHERE order_id = 1;
ROLLBACK TO quantity_test;
RELEASE quantity_test;
COMMIT;

SELECT status FROM orders WHERE order_id = 1;
SELECT quantity FROM order_items WHERE order_id = 1;
```

The status remains changed, while the quantity increase is undone.
