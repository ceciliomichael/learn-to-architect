# Module 11 Exercise

1. Create table `wallet` (`id` INT PRIMARY KEY, `balance` REAL).
2. Insert row `(1, 500.0)`.
3. Open a transaction, deduct `200.0` from wallet 1, set a SAVEPOINT, deduct another `100.0`, then ROLLBACK TO SAVEPOINT and COMMIT.
4. Verify final balance.
