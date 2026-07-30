# Module 11 Exercise Solution

```sql
CREATE TABLE wallet (id INT PRIMARY KEY, balance REAL);
INSERT INTO wallet VALUES (1, 500.0);

BEGIN TRANSACTION;
UPDATE wallet SET balance = balance - 200.0 WHERE id = 1;

SAVEPOINT sp1;
UPDATE wallet SET balance = balance - 100.0 WHERE id = 1;

ROLLBACK TO SAVEPOINT sp1;
COMMIT;

SELECT balance FROM wallet WHERE id = 1;
```

### Expected Output

```text
┌─────────┐
│ balance │
├─────────┤
│ 300.0   │
└─────────┘
```

## Explanation

1. `500.0 - 200.0 = 300.0` was executed before `sp1`.
2. `300.0 - 100.0 = 200.0` was rolled back by `ROLLBACK TO SAVEPOINT sp1`.
3. `COMMIT` persisted the remaining state (`300.0`).
