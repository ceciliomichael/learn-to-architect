# Exercises: Create Tables and Choose SQLite Types

## Exercise 1: Inspect storage classes

Use `typeof` to inspect an integer, real, text, `NULL`, and a byte value written as `X'4142'`.

## Exercise 2: Create a strict table

In `design.db`, create strict `measurements` with:

- `measurement_id` as INTEGER
- `label` as TEXT
- `value` as REAL
- `raw_data` as BLOB

Inspect the schema.

## Exercise 3: Observe enforcement

1. Insert `(1, 'room', 21.5, X'4142')`.
2. Try to insert text `heavy` into `value`.
3. Read the error and confirm only the valid row exists.
