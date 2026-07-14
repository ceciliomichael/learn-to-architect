# Exercises: Use Transactions and Savepoints

## Exercise 1: Prove rollback

In `shop.db`, begin a transaction, change two product prices, inspect them, roll back, and prove both old values returned.

## Exercise 2: Commit one unit

Create a new order and its valid order items in one transaction. Verify the calculated total and commit only if every row is correct.

## Exercise 3: Use a savepoint

Begin a transaction, update an order status, create a savepoint, make an unwanted quantity change, roll back to the savepoint, release it, and commit the status change. Verify both outcomes.
