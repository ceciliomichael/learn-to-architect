# Exercises: Create and Use Views

## Exercise 1: Create a useful view

Create `order_summaries` with one row per order containing order ID, customer, status, and total cents. Include only orders that have items.

## Exercise 2: Prove it is current

1. Query the view.
2. Inside a transaction, add one valid order item.
3. Query the view again and observe the changed total.
4. Roll back and confirm the old total returns.

## Exercise 3: Inspect and remove safely

Inspect the stored view definition, list views through `.tables`, then drop only the practice view. Confirm base order data remains.
