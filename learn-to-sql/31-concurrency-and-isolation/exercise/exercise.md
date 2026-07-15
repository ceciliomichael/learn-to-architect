# Exercises: Concurrency, Locking, and Isolation

## Exercise 1: Observe SQLite writer contention

Open the same disposable database in two SQLite terminals. In connection A, begin immediate and update a row without committing. In B, set a short busy timeout and try another update. Observe the wait or busy error, then roll back A.

## Exercise 2: Separate snapshots from business rules

Write a two-transaction timeline where both sessions read available stock 1 and both try to sell it. State which constraint or atomic update can prevent negative stock.

## Exercise 3: Design a retry boundary

Write pseudocode steps for a PostgreSQL serializable order transaction. Include fresh reads, commit, limited retry, random delay, and an idempotency key.
