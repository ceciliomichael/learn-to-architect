# Exercise Solutions: Protect Data with Constraints and Keys

## Exercise 1

Run the exact `PRAGMA` and two `CREATE TABLE` statements from the lesson. Verify with:

```text
.schema categories
.schema products
```

## Exercise 2

```sql
INSERT INTO categories (category_id, name)
VALUES (1, 'Books');

INSERT INTO categories (category_id, name)
VALUES (2, 'Books');

INSERT INTO products
  (product_id, category_id, name, price_cents, sku)
VALUES
  (1, 99, 'Unknown item', 500, 'UNKNOWN-1');

INSERT INTO products
  (product_id, category_id, name, price_cents, sku)
VALUES
  (2, 1, 'Bad price', -1, 'BAD-PRICE');
```

The duplicate name, missing parent, and negative price statements fail their respective constraints.

## Exercise 3

```sql
INSERT INTO products
  (product_id, category_id, name, price_cents, sku)
VALUES
  (3, 1, 'SQL Guide', 2500, 'BOOK-001');

SELECT product_id, name, active
FROM products;
```

`active` is 1 because the column was omitted and its default supplied that value.
