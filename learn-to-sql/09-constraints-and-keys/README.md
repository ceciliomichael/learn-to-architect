# Module 09: Protect Data with Constraints and Keys

## What you will learn

You will define row identity, required facts, unique values, valid ranges, defaults, and relationships.

## Constraints reject invalid states

Create a fresh `shop.db` and enable SQLite foreign-key enforcement for the connection:

```text
sqlite3 shop.db
```

```sql
PRAGMA foreign_keys = ON;
```

`PRAGMA` is an SQLite-specific SQL extension. SQLite applications should enable foreign keys on every connection unless their framework does it reliably.

## Define a parent table

```sql
CREATE TABLE categories (
  category_id INTEGER PRIMARY KEY,
  name TEXT NOT NULL UNIQUE
) STRICT;
```

- `PRIMARY KEY` gives each row a unique nonmissing identity.
- `NOT NULL` requires a value.
- `UNIQUE` prevents two category rows from using the same name.

In SQLite, `INTEGER PRIMARY KEY` is special: it aliases the internal row identifier and can generate a value when omitted. This exact behavior is SQLite-specific.

## Define checks and defaults

```sql
CREATE TABLE products (
  product_id INTEGER PRIMARY KEY,
  category_id INTEGER NOT NULL,
  name TEXT NOT NULL,
  price_cents INTEGER NOT NULL CHECK (price_cents >= 0),
  active INTEGER NOT NULL DEFAULT 1 CHECK (active IN (0, 1)),
  sku TEXT NOT NULL UNIQUE,
  FOREIGN KEY (category_id) REFERENCES categories(category_id)
) STRICT;
```

`CHECK` requires its expression not to be false. A missing value can pass many checks because the result is unknown, so use `NOT NULL` too when missing is forbidden.

`DEFAULT 1` supplies 1 when an insert omits `active`. It does not override an explicitly supplied `NULL`, which `NOT NULL` rejects.

The foreign key requires each product category to identify an existing category row.

## Composite constraints

A constraint can cover a combination:

```sql
CREATE TABLE shelf_positions (
  shelf_code TEXT NOT NULL,
  position_number INTEGER NOT NULL,
  label TEXT NOT NULL,
  PRIMARY KEY (shelf_code, position_number)
) STRICT;
```

The pair is unique. The same position number can appear on different shelves.

## Constraint failures are useful

If an insert violates a rule, SQLite stops the statement and reports the constraint. Do not silence the error until you understand whether the data or schema rule is wrong.

Check enforcement:

```sql
PRAGMA foreign_keys;
```

It should return 1.

## Choose keys that remain stable

A key should uniquely identify the intended entity and avoid changing during ordinary life. Email addresses and names can change. A generated identifier often works well as the primary key, while business identifiers such as SKU can have separate unique constraints.

## Common mistakes

### Assuming CHECK implies NOT NULL

Unknown can pass a check. Add `NOT NULL` when required.

### Forgetting SQLite foreign-key enforcement

Define the relationships and enable enforcement on every connection.

### Using a changing fact as the primary key

Choose a stable identity and enforce changing business identifiers separately.

## Check your understanding

You are ready when you can state which constraint protects each business rule and explain the difference between a primary and foreign key.
