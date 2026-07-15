# Exercises: Use Triggers Carefully

## Exercise 1: Create and test the audit

Create the lesson audit table and trigger. Update one product price inside a transaction, then inspect the product and audit row.

## Exercise 2: Prove rollback and WHEN behavior

Roll back Exercise 1 and confirm both changes disappear. Then commit an update that assigns the same current price and confirm no audit row is created.

## Exercise 3: Document hidden behavior

Write a short trigger contract stating event, timing, source table, target table, condition, failure effect, and removal command.
