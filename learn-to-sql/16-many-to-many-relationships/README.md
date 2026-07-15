# Module 16: Model Many-to-Many Relationships

## What you will learn

You will represent relationships where each side can connect to many rows and query relationship details.

## Use a junction table

One order can contain many products. One product can appear in many orders. Neither table can hold this relationship in one foreign key.

Create the two new tables in `shop.db`:

```sql
CREATE TABLE orders (
  order_id INTEGER PRIMARY KEY,
  customer_name TEXT NOT NULL,
  status TEXT NOT NULL CHECK (status IN ('open', 'paid', 'cancelled'))
) STRICT;

CREATE TABLE order_items (
  order_id INTEGER NOT NULL,
  product_id INTEGER NOT NULL,
  quantity INTEGER NOT NULL CHECK (quantity > 0),
  unit_price_cents INTEGER NOT NULL CHECK (unit_price_cents >= 0),
  PRIMARY KEY (order_id, product_id),
  FOREIGN KEY (order_id) REFERENCES orders(order_id),
  FOREIGN KEY (product_id) REFERENCES products(product_id)
) STRICT;
```

`order_items` is the junction table. Its composite primary key prevents the same product appearing twice in one order. Quantity and price belong to the relationship at purchase time.

## Query through the junction

```sql
SELECT
  o.order_id,
  o.customer_name,
  p.name AS product_name,
  oi.quantity,
  oi.unit_price_cents
FROM orders AS o
JOIN order_items AS oi
  ON oi.order_id = o.order_id
JOIN products AS p
  ON p.product_id = oi.product_id
ORDER BY o.order_id, p.name;
```

The result grain is one order item. Each join follows one declared foreign key.

## Calculate order totals

```sql
SELECT
  o.order_id,
  o.customer_name,
  SUM(oi.quantity * oi.unit_price_cents) AS total_cents
FROM orders AS o
JOIN order_items AS oi
  ON oi.order_id = o.order_id
GROUP BY o.order_id, o.customer_name
ORDER BY o.order_id;
```

The price is stored on `order_items` because the current product price may change after purchase.

## Find products never ordered

```sql
SELECT p.product_id, p.name
FROM products AS p
LEFT JOIN order_items AS oi
  ON oi.product_id = p.product_id
WHERE oi.order_id IS NULL;
```

## Do not store comma-separated identifiers

A column such as `product_ids = '1,4,9'` cannot use ordinary foreign keys, is hard to search safely, and allows duplicates or invalid text. One junction row per relationship keeps facts queryable and protected.

## Common mistakes

### Omitting a key from the junction

Duplicate relationship rows can inflate totals. Use a suitable composite primary or unique key.

### Taking historical price from products

Store the agreed purchase price on the order item when history must remain accurate.

### Joining both sides directly

Orders and products relate through `order_items`; follow both foreign keys.

## Check your understanding

You are ready when you can identify a many-to-many relationship, design its junction table, and state the grain of a three-table result.
