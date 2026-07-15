# Module 29: Upsert, RETURNING, and Generated Values

## What you will learn

You will handle a specific uniqueness conflict, return changed rows, and define values calculated from other columns.

## Upsert means insert or respond to one conflict

SQLite follows PostgreSQL-style upsert syntax with SQLite-specific details:

```sql
INSERT INTO inventory (product_id, quantity)
VALUES (1, 5)
ON CONFLICT (product_id) DO UPDATE
SET quantity = inventory.quantity + excluded.quantity;
```

If product 1 is absent, SQLite inserts it. If the named uniqueness rule conflicts, `excluded.quantity` is the proposed value and the update adds it to the existing quantity.

Name the conflict target. Do not use conflict handling to hide unrelated `NOT NULL`, check, or foreign-key errors.

## Add a condition to the update

```sql
INSERT INTO inventory (product_id, quantity)
VALUES (1, 5)
ON CONFLICT (product_id) DO UPDATE
SET quantity = inventory.quantity + excluded.quantity
WHERE excluded.quantity > 0;
```

If the condition is false, the conflicting row is left unchanged.

## Return changed values

```sql
INSERT INTO inventory (product_id, quantity)
VALUES (2, 3)
ON CONFLICT (product_id) DO UPDATE
SET quantity = inventory.quantity + excluded.quantity
RETURNING product_id, quantity;
```

SQLite `RETURNING` reports rows changed by top-level insert, update, or delete statements. It does not include additional rows changed by triggers and has documented limitations compared with PostgreSQL.

## Generated columns calculate row values

```sql
CREATE TABLE invoice_lines (
  line_id INTEGER PRIMARY KEY,
  quantity INTEGER NOT NULL CHECK (quantity > 0),
  unit_price_cents INTEGER NOT NULL CHECK (unit_price_cents >= 0),
  line_total_cents INTEGER
    GENERATED ALWAYS AS (quantity * unit_price_cents) STORED
) STRICT;
```

A virtual generated value is calculated when read. A stored generated value is calculated when written and stored. The expression can use deterministic scalar functions and columns in the same row, but not subqueries, aggregates, or window functions.

Do not insert directly into the generated column:

```sql
INSERT INTO invoice_lines (quantity, unit_price_cents)
VALUES (2, 350)
RETURNING line_id, line_total_cents;
```

Generated columns protect calculation consistency, but changing their expression requires a schema migration and product-specific planning.

## Choose between generated data and query expressions

Use a query expression when the calculation belongs only to a report or changes often. Consider a generated column when the row-level calculation is stable, reused, and benefits from indexing or centralized consistency.

## Common mistakes

### Using replace as a universal upsert

SQLite `REPLACE` can delete a conflicting row and insert another, which can affect identifiers, triggers, and relationships. Use explicit `ON CONFLICT DO UPDATE` behavior.

### Omitting the intended conflict target

State which uniqueness rule permits the update.

### Generating a value from another table

SQLite generated expressions are row-local. Use a query, trigger, or deliberate stored process for cross-table behavior.

## Check your understanding

You are ready when you can explain `excluded`, predict insert versus update, and choose a generated or query-time value from its meaning.
