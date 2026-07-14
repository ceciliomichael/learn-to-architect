# Module 28: Change Schemas with Migrations

## What you will learn

You will evolve a schema through versioned, tested changes instead of editing production tables by hand.

## A migration is a recorded schema change

A migration is an ordered script that moves a known schema version to the next version. Teams store migration files with application code and run each version once through a migration tool or controlled process.

Good migrations are:

- Complete and reviewable
- Tested on a production-like copy
- Safe for existing rows
- Observable during deployment
- Recorded as applied only after success

## Back up before SQLite practice

In the SQLite CLI:

```text
.backup shop-before-migration.db
```

`.backup` is a CLI command, not SQL. Verify that the backup file exists and can be opened. A backup is useful only if restore has been tested.

## Simple ALTER TABLE changes

Current SQLite supports renaming a table or column, adding a column, and dropping a column under documented restrictions:

```sql
ALTER TABLE products ADD COLUMN description TEXT;
ALTER TABLE products RENAME COLUMN description TO details;
```

Adding a required column to existing rows needs a valid backfill strategy. A common safe sequence is:

1. Add it as nullable or with a safe default.
2. Deploy code that can handle both schema states.
3. Backfill existing rows in controlled batches.
4. Enforce the final constraint in a later migration.

## Rebuild a table for broader changes

SQLite documents a table-rebuild approach when direct alteration cannot express the change:

1. Record dependent views, triggers, and indexes.
2. Disable foreign-key enforcement before the transaction when the migration requires it.
3. Begin a transaction.
4. Create a new table with the desired schema.
5. Copy and transform existing data with explicit columns.
6. Drop the old table.
7. Rename the new table.
8. Recreate indexes, triggers, and views.
9. Check foreign keys and schema.
10. Commit, re-enable enforcement, and test.

A simplified disposable example is:

```sql
PRAGMA foreign_keys = OFF;
BEGIN;

CREATE TABLE products_new (
  product_id INTEGER PRIMARY KEY,
  category_id INTEGER NOT NULL,
  name TEXT NOT NULL,
  price_cents INTEGER NOT NULL CHECK (price_cents >= 0),
  active INTEGER NOT NULL DEFAULT 1 CHECK (active IN (0, 1)),
  sku TEXT NOT NULL UNIQUE,
  details TEXT,
  FOREIGN KEY (category_id) REFERENCES categories(category_id)
) STRICT;

INSERT INTO products_new
  (product_id, category_id, name, price_cents, active, sku, details)
SELECT
  product_id, category_id, name, price_cents, active, sku, NULL
FROM products;

DROP TABLE products;
ALTER TABLE products_new RENAME TO products;

COMMIT;
PRAGMA foreign_keys = ON;
PRAGMA foreign_key_check;
```

Real migrations must recreate any indexes, triggers, and views associated with the old table. Never improvise this on a live database.

## Forward and backward safety

Some changes cannot be reversed without lost data. A rollback script that recreates a dropped column cannot recover its old values. Prefer forward fixes and backups over claiming every migration is reversible.

For deployed services, schema and application versions may overlap. Expand first, move data and code, then contract old structures in a later release.

## Common mistakes

### Editing an applied migration

Other databases may already record the old content. Add a new migration.

### Adding NOT NULL without existing-row handling

Plan the default or backfill before enforcement.

### Rebuilding without dependencies

Indexes, triggers, and views can disappear or break. Inventory and recreate them.

## Check your understanding

You are ready when you can explain an expand-backfill-contract sequence and list every object affected by a table rebuild.
