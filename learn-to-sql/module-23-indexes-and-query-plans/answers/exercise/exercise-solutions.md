# Exercise Solutions: Create Indexes and Read Query Plans

## Exercise 1

```sql
EXPLAIN QUERY PLAN
SELECT product_id, name FROM products WHERE category_id = 2;

CREATE INDEX products_category_idx ON products (category_id);

EXPLAIN QUERY PLAN
SELECT product_id, name FROM products WHERE category_id = 2;
```

The later plan may report an index search. A tiny table can still make scanning reasonable.

## Exercise 2

```sql
CREATE INDEX products_category_active_price_idx
ON products (category_id, active, price_cents);

EXPLAIN QUERY PLAN
SELECT name FROM products
WHERE category_id = 2 AND active = 1 AND price_cents >= 200;

EXPLAIN QUERY PLAN
SELECT name FROM products WHERE price_cents >= 200;
```

The first follows the leftmost equality columns. The second lacks conditions on the leftmost prefix.

## Exercise 3

```text
.indexes products
```

Changing price may update any index containing `price_cents`, including partial indexes when membership changes. Clean up the practice indexes:

```sql
DROP INDEX IF EXISTS products_category_idx;
DROP INDEX IF EXISTS products_category_active_price_idx;
```
