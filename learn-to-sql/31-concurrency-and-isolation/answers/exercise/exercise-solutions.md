# Exercise Solutions: Concurrency, Locking, and Isolation

## Exercise 1

Connection A:

```sql
BEGIN IMMEDIATE;
UPDATE products SET price_cents = price_cents + 1 WHERE product_id = 1;
```

Connection B:

```sql
PRAGMA busy_timeout = 1000;
UPDATE products SET price_cents = price_cents + 1 WHERE product_id = 2;
```

B waits up to about one second and then may report a locked or busy database. Run `ROLLBACK;` in A. This is a disposable observation only.

## Exercise 2

Use one atomic statement such as `UPDATE inventory SET quantity = quantity - 1 WHERE product_id = ? AND quantity >= 1`, then require an affected row count of 1. A `CHECK(quantity >= 0)` supplies another database guard. The transaction must treat a zero-row update as unavailable stock.

## Exercise 3

Accept a unique request key, begin serializable, check whether that key already completed, reread products and stock, create the order and items, commit, and return the stored result. On serialization or deadlock error, roll back, wait a bounded random delay, and retry the entire function a limited number of times.
