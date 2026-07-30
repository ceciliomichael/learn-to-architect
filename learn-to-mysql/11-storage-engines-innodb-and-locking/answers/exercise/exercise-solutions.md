# Module 11 Exercise Solution

```sql
START TRANSACTION;

INSERT INTO `accounts` (`id`, `balance`) VALUES (1, 1000.00);

SAVEPOINT `sp1`;

UPDATE `accounts` SET `balance` = 500.00 WHERE `id` = 1;

ROLLBACK TO SAVEPOINT `sp1`;

COMMIT;

SELECT `balance` FROM `accounts` WHERE `id` = 1;
```

### Expected Output

```text
+---------+
| balance |
+---------+
| 1000.00 |
+---------+
```

## Explanation

1. The initial insert of 1000.00 occurs before `sp1`.
2. The update to 500.00 is rolled back by `ROLLBACK TO SAVEPOINT sp1`.
3. `COMMIT` finalizes the transaction, keeping balance at 1000.00.
