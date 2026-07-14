# Exercise Solutions: Tune Queries with Evidence

## Exercise 1

One valid requirement is: with 500,000 products, 100 categories, realistic active-value skew, and 20 concurrent sessions, return the first 50 active products for one category ordered by price within 80 ms at the 95th percentile, while sustaining 100 product writes per second.

## Exercise 2

Baseline and candidate plan statements are:

```sql
EXPLAIN QUERY PLAN
SELECT product_id, name, price_cents
FROM products
WHERE category_id = 2 AND active = 1
ORDER BY price_cents, product_id
LIMIT 50;

CREATE INDEX products_active_category_price_idx
ON products (category_id, price_cents, product_id)
WHERE active = 1;
```

Repeat the exact plan and timed query. Also time a representative insert batch because the index adds maintenance.

## Exercise 3

Use a read-only select first. Record plan nodes, estimated rows, actual rows, loops, execution time, and buffer activity. A valid hypothesis might be stale statistics or a missing selective index. Apply only one change, run `ANALYZE` if appropriate, and compare the same workload and cache conditions.
