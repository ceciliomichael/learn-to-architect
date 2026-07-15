# Exercise Solutions: Upsert, RETURNING, and Generated Values

## Exercise 1

```sql
CREATE TABLE inventory (
  product_id INTEGER PRIMARY KEY,
  quantity INTEGER NOT NULL CHECK (quantity >= 0),
  FOREIGN KEY (product_id) REFERENCES products(product_id)
) STRICT;
INSERT INTO inventory VALUES (1, 5);
```

Use an existing product identifier.

## Exercise 2

```sql
INSERT INTO inventory (product_id, quantity) VALUES (1, 3)
ON CONFLICT (product_id) DO UPDATE
SET quantity = inventory.quantity + excluded.quantity
RETURNING product_id, quantity;

INSERT INTO inventory (product_id, quantity) VALUES (2, 4)
ON CONFLICT (product_id) DO UPDATE
SET quantity = inventory.quantity + excluded.quantity
RETURNING product_id, quantity;
```

The first updates to 8 and the second inserts 4, assuming those starting values. A negative final quantity violates the check.

## Exercise 3

Create the exact lesson table, then:

```sql
INSERT INTO invoice_lines (quantity, unit_price_cents)
VALUES (2, 350), (1, 999), (4, 125);
SELECT * FROM invoice_lines;
UPDATE invoice_lines SET quantity = 3 WHERE line_id = 1;
SELECT * FROM invoice_lines WHERE line_id = 1;
```

The first total changes from 700 to 1050 automatically.
