# Exercises: Change Schemas with Migrations

Use a copied disposable `shop.db`.

## Exercise 1: Back up and add safely

1. Create a SQLite backup.
2. Add nullable `details` to products.
3. Backfill two known products inside a transaction.
4. Inspect schema and data.

## Exercise 2: Rebuild a practice table

Create a small `legacy_notes(note_id, body)` table with rows. Rebuild it as a strict table with required body and optional created date. Copy rows, validate counts, and commit.

## Exercise 3: Plan an online change

Write an expand, backfill, code switch, and contract plan for replacing `customer_name` with a customer foreign key. Identify compatibility and rollback risks without executing it.
