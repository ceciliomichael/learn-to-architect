# Exercise Solutions: Insert Rows

## Exercise 1

```sql
PRAGMA foreign_keys = ON;

INSERT INTO categories (name)
VALUES ('Electronics')
RETURNING category_id, name;

SELECT category_id, name
FROM categories
ORDER BY category_id;
```

Your generated identifier depends on existing rows.

## Exercise 2

Use identifiers from your category result. One valid example is:

```sql
INSERT INTO products
  (category_id, name, price_cents, sku)
VALUES
  (1, 'Query Cards', 800, 'BOOK-003'),
  (2, 'Black Pen', 250, 'PEN-BLACK'),
  (3, 'USB Lamp', 1800, 'LAMP-USB');

SELECT product_id, name, price_cents, active, sku
FROM products
ORDER BY product_id;
```

Adjust category identifiers if your database differs. Each active value should be 1.

## Exercise 3

```sql
INSERT INTO products
  (category_id, name, price_cents, sku)
VALUES
  (2, 'Red Pen', 250, 'DUPLICATE-SKU'),
  (2, 'Green Pen', 250, 'DUPLICATE-SKU');
```

The unique constraint rejects the statement. Verify zero matching rows:

```sql
SELECT * FROM products
WHERE sku = 'DUPLICATE-SKU';
```

Change one SKU and rerun the two-row statement.
