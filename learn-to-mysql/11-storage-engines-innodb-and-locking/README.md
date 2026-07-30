# Module 11: Storage Engines (InnoDB), Locking, and Transaction Control

## What You Will Learn

In this module, you will learn how MySQL's pluggable storage engine architecture works (comparing InnoDB vs. MyISAM), control transactions using `START TRANSACTION`, `COMMIT`, and `ROLLBACK`, manage transaction isolation levels (`READ COMMITTED`, `REPEATABLE READ`), and handle row-level locking.

---

## InnoDB vs MyISAM Storage Engines

| Feature | InnoDB (Default) | MyISAM (Legacy) |
| :--- | :--- | :--- |
| **ACID Transactions** | Yes (`START TRANSACTION`) | No |
| **Locking Granularity** | Row-level locking | Table-level locking |
| **Foreign Keys** | Fully Supported | Not Supported |
| **Crash Recovery** | Automatic via redo logs | Manual repair table |

---

## Transaction Control Statements

```sql
START TRANSACTION;

UPDATE `accounts` SET `balance` = `balance` - 500.00 WHERE `id` = 1;
UPDATE `accounts` SET `balance` = `balance` + 500.00 WHERE `id` = 2;

-- Confirm changes
COMMIT;

-- Or revert changes if error occurs
-- ROLLBACK;
```

---

## Transaction Isolation Levels

MySQL InnoDB defaults to **`REPEATABLE READ`**:

1. `READ UNCOMMITTED` (Allows dirty reads)
2. `READ COMMITTED` (Prevents dirty reads)
3. `REPEATABLE READ` (Default in MySQL - prevents non-repeatable reads)
4. `SERIALIZABLE` (Strict full table/range locking)

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

---

## Check Your Understanding

1. What is the default transaction isolation level in MySQL InnoDB?
2. What happens when two concurrent transactions attempt to `UPDATE` the exact same row under InnoDB row-level locking?
