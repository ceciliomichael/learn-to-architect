# Exercises: Insert Rows

Use `shop.db` and enable foreign keys.

## Exercise 1: Add parents

1. Insert `Electronics` without choosing its identifier.
2. Use `RETURNING` to read the generated identifier and name.
3. Select all categories in identifier order.

## Exercise 2: Add several products

Insert three valid products in one statement. Use existing category identifiers, unique SKUs, nonnegative prices, and omit `active`.

Verify every inserted row and its default.

## Exercise 3: Learn from a failed statement

Try a two-row insert where the second row repeats the first row's SKU. Confirm neither row from that statement was inserted. Correct the SKU and try again.
