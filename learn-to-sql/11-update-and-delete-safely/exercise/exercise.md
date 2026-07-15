# Exercises: Update and Delete Rows Safely

Use only `shop.db`.

## Exercise 1: Preview and update one row

1. Begin a transaction.
2. Preview one product by its unique SKU.
3. Increase its price by 50 cents.
4. Check `changes()` and select the row again.
5. Roll back and prove the old price returned.

## Exercise 2: Update a chosen group

1. Select all active products for one category.
2. Begin a transaction and set only those rows inactive.
3. Verify the group and affected count.
4. Commit if the result matches the preview.

## Exercise 3: Delete with expected state

1. Choose one disposable inactive product.
2. Preview it by primary key and `active = 0`.
3. Delete with the same two conditions inside a transaction.
4. Verify it is absent, then roll back so the practice row returns.
