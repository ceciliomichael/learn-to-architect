# Module 11: Manage Transactions and Savepoints

## What You Will Learn

In this module, you will learn how to group multiple database operations into atomic, ACID-compliant transactions using `BEGIN TRANSACTION`, `COMMIT`, and `ROLLBACK`, manage nested logic with `SAVEPOINT`, and configure Write-Ahead Logging (`PRAGMA journal_mode=WAL;`).

---

## Transaction Basics: ACID Guarantees

A transaction is a unit of work that succeeds completely or fails completely.

- `BEGIN TRANSACTION`: Starts a transaction block.
- `COMMIT`: Saves all mutations permanently to disk.
- `ROLLBACK`: Reverts all mutations back to the state prior to `BEGIN TRANSACTION`.

```sql
BEGIN TRANSACTION;

UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

-- If everything is valid:
COMMIT;
```

---

## Savepoints (Nested Transactions)

Savepoints allow rolling back to a specific checkpoint inside a transaction:

```sql
SAVEPOINT step1;

UPDATE inventory SET stock = stock - 1 WHERE id = 10;

-- Rollback only to step1:
ROLLBACK TO SAVEPOINT step1;
RELEASE SAVEPOINT step1;
```

---

## Write-Ahead Logging (WAL Mode)

By default, SQLite uses a rollback journal for concurrency. Enabling WAL mode improves concurrent read/write performance:

```sql
PRAGMA journal_mode = WAL;
```

---

## Check Your Understanding

1. What happens to database changes if an error occurs before `COMMIT` and `ROLLBACK` is issued?
2. How does WAL mode (`PRAGMA journal_mode = WAL;`) affect readers and writers?
