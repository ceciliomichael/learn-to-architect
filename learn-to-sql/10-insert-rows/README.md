# Module 10: Insert Rows

## What you will learn

You will add one or many rows with explicit columns, use defaults, and inspect generated identifiers.

## Name the columns

In `shop.db` with foreign keys enabled:

```sql
INSERT INTO categories (name)
VALUES ('Stationery');
```

The `INTEGER PRIMARY KEY` is omitted, so SQLite generates it. Explicit column lists protect the statement if table column order later changes.

## Read the generated row

SQLite 3.35 and newer supports `RETURNING`:

```sql
INSERT INTO categories (name)
VALUES ('Games')
RETURNING category_id, name;
```

`RETURNING` is supported by several products but is not identical everywhere. In SQLite, it returns values from rows changed by that top-level statement.

The SQLite CLI also provides `last_insert_rowid()`, but it is connection-specific and easy to misuse when triggers or other inserts are involved. Prefer `RETURNING` when it fits.

## Insert several rows

```sql
INSERT INTO products
  (category_id, name, price_cents, sku)
VALUES
  (1, 'Database Notebook', 1200, 'BOOK-002'),
  (2, 'Blue Pen', 250, 'PEN-BLUE'),
  (2, 'Grid Pad', 450, 'PAD-GRID');
```

The statement is atomic: either all its rows succeed or the statement fails. A larger transaction can group several statements, taught in Module 21.

## Use defaults by omission

The products omit `active`, so its default 1 is used. You can also write `DEFAULT` in some SQL products, but SQLite does not support every multi-row default syntax found elsewhere. Omission is clear here.

## Insert from a query

SQL can insert selected rows:

```sql
CREATE TABLE active_product_names (
  product_name TEXT NOT NULL
) STRICT;

INSERT INTO active_product_names (product_name)
SELECT name
FROM products
WHERE active = 1;
```

The selected column count and values must fit the target list.

## Handle failures rather than hiding them

SQLite offers conflict behaviors such as `OR IGNORE` and upsert syntax. Do not use them as a general way to suppress errors. Module 29 teaches how to choose a conflict target and intended outcome.

## Common mistakes

### Omitting the target column list

The statement becomes coupled to physical column order and is hard to review.

### Quoting numbers as text

Write numeric values without text quotes. Strict tables help reject bad conversions.

### Assuming every generated key method is portable

Identity behavior and return syntax differ. Use the target product's documented method.

## Check your understanding

You are ready when you can insert one and several valid rows, predict defaults, and retrieve a generated SQLite identifier safely.
