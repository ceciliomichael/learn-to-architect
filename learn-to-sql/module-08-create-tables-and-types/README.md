# Module 08: Create Tables and Choose SQLite Types

## What you will learn

You will create tables deliberately and understand SQLite storage classes, type affinity, and `STRICT` tables.

## A schema is a data agreement

A table definition should describe facts and their intended form. Good names and types help readers, tools, and constraints protect that agreement.

Create a new disposable database:

```text
sqlite3 design.db
```

## SQLite values have storage classes

SQLite values use five storage classes:

- `NULL` for missing information
- `INTEGER` for whole numbers
- `REAL` for floating-point numbers
- `TEXT` for text
- `BLOB` for bytes stored exactly as supplied

In ordinary SQLite tables, the value has a storage class and the column has a type affinity. Affinity is SQLite's preference for converting inserted values. It is not the same as the strict column typing used by PostgreSQL.

Common declared names produce INTEGER, TEXT, REAL, NUMERIC, or BLOB affinity according to SQLite's documented rules. This means a surprising name can produce a surprising affinity. Use simple intentional names.

## Create an ordinary table

```sql
CREATE TABLE products (
  product_id INTEGER,
  name TEXT,
  price_cents INTEGER,
  weight REAL,
  photo BLOB
);
```

Each definition has a column name and declared type. The semicolon ends the whole statement.

Inspect it:

```text
.schema products
```

Delete this disposable empty table so you can replace it:

```sql
DROP TABLE products;
```

`DROP TABLE` removes the table and its data. It is safe here only because the table is empty and disposable.

## Use STRICT when its smaller type set fits

SQLite supports `STRICT` tables:

```sql
CREATE TABLE products (
  product_id INTEGER,
  name TEXT,
  price_cents INTEGER,
  weight REAL,
  photo BLOB
) STRICT;
```

A strict table accepts declared types `INT`, `INTEGER`, `REAL`, `TEXT`, `BLOB`, and `ANY`. It rejects values that cannot be converted without loss to the declared type. `ANY` preserves any SQLite storage class.

Strict mode still does not turn SQLite into PostgreSQL. It provides stronger enforcement within SQLite's model.

## Check a value's storage class

SQLite's `typeof` function reports the stored class:

```sql
SELECT
  typeof(12) AS whole_number,
  typeof(12.5) AS real_number,
  typeof('12') AS text_value,
  typeof(NULL) AS missing_value;
```

This is an SQLite function, not portable SQL.

## Choose representations from meaning

- Store counts and identifiers as `INTEGER`.
- Store human text as `TEXT`.
- Use integer minor units such as cents when exact fixed-scale SQLite money arithmetic is required and rules permit it.
- Use `REAL` for approximate measurements where floating-point behavior is acceptable.
- Store dates consistently, a topic in Module 26.
- Do not store several facts in one comma-separated text column.

Type choice is only one part of design. Module 09 adds required values, uniqueness, ranges, and relationships.

## Common mistakes

### Assuming `VARCHAR(20)` enforces length in SQLite

SQLite does not enforce the number in that declared name. Add a `CHECK` constraint when length is a real rule.

### Storing exact money in REAL without a decision

Floating-point values are approximate. Choose a representation from the business rules.

### Using DROP on a valuable table

It removes data. Practice only in `design.db` and use migrations and backups for real schemas.

## Check your understanding

You are ready when you can name SQLite's storage classes, explain affinity, and state what `STRICT` adds.
