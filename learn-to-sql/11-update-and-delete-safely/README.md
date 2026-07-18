# Module 11: Update and Delete Rows Safely

## What you will learn

You will preview target rows, update exact columns, delete exact rows, and recover with a transaction.

## Use a safety routine

Before changing existing rows:

1. Confirm the database with `.databases`.
2. Start a transaction.
3. Write a `SELECT` with the intended `WHERE`.
4. Inspect identifiers and current values.
5. Use the same condition in `UPDATE` or `DELETE`.
6. Inspect the changed rows.
7. Commit only when correct, otherwise roll back.

## Update selected rows

Preview:

```sql
SELECT product_id, name, price_cents
FROM products
WHERE sku = 'PEN-BLUE';
```

Then change the selected row:

```sql
UPDATE products
SET price_cents = 275
WHERE sku = 'PEN-BLUE';
```

Use `changes()` immediately in SQLite to see how many rows the previous data-changing statement affected:

```sql
SELECT changes() AS changed_rows;
```

`changes()` is SQLite-specific.

## Update from the old value

```sql
UPDATE products
SET price_cents = price_cents + 100
WHERE category_id = 1;
```

Each matching row uses its own old price. Preview all category 1 rows first.

## Delete selected rows

Preview an inactive row:

```sql
SELECT product_id, name, active
FROM products
WHERE product_id = 7
  AND active = 0;
```

Only when the preview is correct:

```sql
DELETE FROM products
WHERE product_id = 7
  AND active = 0;
```

Using a stable identifier plus an expected state prevents deleting a row that changed unexpectedly.

## Protect the work with a transaction

```sql
BEGIN;

UPDATE products
SET active = 0
WHERE category_id = 2;

SELECT product_id, name, active
FROM products
WHERE category_id = 2;

ROLLBACK;
```

`ROLLBACK` returns the database to its state before `BEGIN`. Replace it with `COMMIT` only after verification.

## A missing WHERE changes every row

These are valid but broad:

```sql
UPDATE products SET active = 0;
DELETE FROM products;
```

They affect all rows. Never add a fake condition such as `WHERE 1 = 1` to make broad changes look safer. If all rows truly need a change, state that purpose, use a transaction, count them before and after, and obtain the required review.

## Foreign keys can block deletes

Deleting a category referenced by products fails under the current default relationship. Other actions such as cascading deletes must be designed explicitly. A blocked delete protects connected data.

## Common mistakes

### Previewing with a different condition

Copy the exact predicate and review it again in the change statement.

### Committing before checking row count

Inspect affected rows and `changes()` inside the transaction.

### Treating a backup as permission to be careless

Restores take time and can lose later work. Prevent the mistake first.

## Check your understanding

You are ready when you can make one precise update inside a transaction and choose commit or rollback from evidence.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
