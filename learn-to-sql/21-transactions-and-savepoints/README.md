# Module 21: Use Transactions and Savepoints

## What you will learn

You will group changes atomically, choose commit or rollback, and create recovery points inside a transaction.

## A transaction is one unit of work

Atomic means all intended statements commit together or none of them do. Transfer-style work shows why:

```sql
BEGIN;

UPDATE accounts
SET balance_cents = balance_cents - 1000
WHERE account_id = 1
  AND balance_cents >= 1000;

UPDATE accounts
SET balance_cents = balance_cents + 1000
WHERE account_id = 2;

COMMIT;
```

Real code must verify both accounts and the first update's row count before committing. A transaction does not make incorrect logic correct. It provides a boundary for validation and rollback.

## Commit or roll back

```sql
BEGIN;
UPDATE products SET price_cents = price_cents + 50 WHERE category_id = 1;
SELECT * FROM products WHERE category_id = 1;
ROLLBACK;
```

`COMMIT` makes the transaction's changes durable. `ROLLBACK` abandons them.

SQLite automatically uses implicit transactions for standalone statements. Explicit transactions are needed when several statements form one decision or when you want to inspect before committing.

## Savepoints create inner recovery points

SQLite does not nest independent `BEGIN` transactions. Use savepoints:

```sql
BEGIN;

UPDATE orders SET status = 'paid' WHERE order_id = 1;

SAVEPOINT item_changes;
UPDATE order_items SET quantity = quantity + 1 WHERE order_id = 1;

ROLLBACK TO item_changes;
RELEASE item_changes;

COMMIT;
```

`ROLLBACK TO` undoes work after the savepoint but keeps the transaction active. `RELEASE` removes that savepoint. The earlier order update remains available to commit.

## SQLite transaction modes

```sql
BEGIN DEFERRED;
BEGIN IMMEDIATE;
BEGIN EXCLUSIVE;
```

- Deferred is the default and does not start a write transaction until needed.
- Immediate attempts to begin a write transaction immediately and can fail if another writer is active.
- Exclusive is similar to immediate in write-ahead logging mode, but blocks more access in other journal modes.

Choose from concurrency needs, not habit. Module 31 explains locking and retries.

## Keep transactions short

Do not wait for user input or perform slow network work while holding a database transaction. Long transactions retain locks or old snapshots, increase contention, and delay cleanup.

## Handle errors explicitly

Constraint errors can abort a statement while leaving an explicit SQLite transaction active, depending on conflict behavior. Applications must catch errors and deliberately commit or roll back. Do not assume every error automatically closes the transaction.

## Common mistakes

### Starting BEGIN inside BEGIN

Use savepoints for nested recovery.

### Believing a transaction validates business logic

Check row counts, balances, constraints, and expected states.

### Leaving a transaction open

Every code path should finish with commit or rollback.

## Check your understanding

You are ready when you can group related changes, verify them before commit, and roll back only the work after a savepoint.
