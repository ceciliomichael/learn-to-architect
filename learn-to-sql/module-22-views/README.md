# Module 22: Create and Use Views

## What you will learn

You will store a query definition under a name and understand its benefits and limits.

## A view is a stored query

```sql
CREATE VIEW active_product_details AS
SELECT
  p.product_id,
  p.name AS product_name,
  c.name AS category_name,
  p.price_cents
FROM products AS p
JOIN categories AS c ON c.category_id = p.category_id
WHERE p.active = 1;
```

Query it like a table:

```sql
SELECT product_name, category_name, price_cents
FROM active_product_details
ORDER BY product_name;
```

SQLite stores the query definition, not a separate copy of its result. Changes to base tables appear the next time the view is queried.

## Views create a named interface

A useful view can:

- Give one name to a repeated join or filter
- Expose a smaller, clearer column set
- Separate consumers from some underlying query complexity
- Support permissions in server databases when designed correctly

A view is not automatically a security boundary. SQLite has no role-based table permissions, and PostgreSQL view security depends on ownership and options.

## Choose clear output names

Name every ambiguous or calculated result column. SQLite allows an explicit view column list:

```sql
CREATE VIEW product_prices (product_id, product_name, price_cents) AS
SELECT product_id, name, price_cents
FROM products;
```

Stable explicit names are better than relying on generated expression names.

## SQLite views are read-only by default

SQLite does not directly allow ordinary insert, update, or delete against a view. `INSTEAD OF` triggers can implement behavior, but that creates hidden write logic and needs careful tests. PostgreSQL supports automatically updatable views under documented conditions.

## Replace through a migration

SQLite has no general `CREATE OR REPLACE VIEW`. Change one inside a migration:

```sql
BEGIN;
DROP VIEW active_product_details;
CREATE VIEW active_product_details AS
SELECT
  p.product_id,
  p.name AS product_name,
  c.name AS category_name,
  p.price_cents
FROM products AS p
JOIN categories AS c ON c.category_id = p.category_id
WHERE p.active = 1;
COMMIT;
```

Real migrations must contain the full new query, check dependents, and use a backup.

## Inspect and remove

```text
.schema active_product_details
```

```sql
DROP VIEW active_product_details;
```

Dropping the view removes the definition, not the base table rows.

## Common mistakes

### Assuming a view stores fresh copied data

Ordinary SQLite views run their query when read.

### Depending on SELECT star in a shared interface

Name the intended output columns so schema changes are deliberate.

### Hiding a very slow query behind a view

The work still runs. Inspect plans and workload.

## Check your understanding

You are ready when you can create a named read interface and explain why it is neither a copied result nor automatic security.
