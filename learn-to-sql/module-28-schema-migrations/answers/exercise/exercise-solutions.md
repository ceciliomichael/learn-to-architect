# Exercise Solutions: Change Schemas with Migrations

## Exercise 1

```text
.backup shop-before-details.db
```

```sql
ALTER TABLE products ADD COLUMN details TEXT;
BEGIN;
UPDATE products SET details = 'Practice detail' WHERE product_id IN (1, 2);
SELECT product_id, details FROM products WHERE product_id IN (1, 2);
COMMIT;
```

Inspect with `.schema products` and a complete select.

## Exercise 2

```sql
CREATE TABLE legacy_notes (note_id INTEGER PRIMARY KEY, body TEXT);
INSERT INTO legacy_notes VALUES (1, 'First'), (2, 'Second');

BEGIN;
CREATE TABLE notes_new (
  note_id INTEGER PRIMARY KEY,
  body TEXT NOT NULL,
  created_date TEXT
) STRICT;
INSERT INTO notes_new (note_id, body, created_date)
SELECT note_id, body, NULL FROM legacy_notes;
SELECT COUNT(*) FROM notes_new;
DROP TABLE legacy_notes;
ALTER TABLE notes_new RENAME TO legacy_notes;
COMMIT;
```

The count must match before the drop.

## Exercise 3

Add customers and a nullable `customer_id`, deploy code that writes both old name and new ID, backfill and verify IDs, switch all readers to the relationship, then remove the old text only in a later migration. Rollback becomes harder after removing the old source, so delay contraction and keep tested backups.
