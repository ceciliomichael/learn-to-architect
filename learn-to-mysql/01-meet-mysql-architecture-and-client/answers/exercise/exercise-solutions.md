# Module 01 Exercise Solution

```sql
CREATE DATABASE store_db;
USE store_db;

SELECT USER() AS current_user, DATABASE() AS active_db;
```

### Expected Output

```text
+----------------+-----------+
| current_user   | active_db |
+----------------+-----------+
| root@localhost | store_db  |
+----------------+-----------+
```

## Explanation

1. `CREATE DATABASE store_db;` creates a logical database namespace.
2. `USE store_db;` switches the connection context to `store_db`.
3. `USER()` and `DATABASE()` are MySQL built-in system functions.
