# Module 11 Exercise

1. Open a transaction using `START TRANSACTION;`.
2. Insert 1 row into `accounts`, set a SAVEPOINT `sp1`, update balance, then `ROLLBACK TO SAVEPOINT sp1;`.
3. Commit transaction and inspect final row.
