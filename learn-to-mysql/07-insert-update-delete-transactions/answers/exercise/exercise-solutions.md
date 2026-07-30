# Module 07 Exercise Solution

```sql
INSERT INTO `users` SET `username` = 'eve', `email` = 'eve@example.com', `role` = 'user';
INSERT INTO `users` SET `username` = 'frank', `email` = 'frank@example.com', `role` = 'user';

-- Preview Step:
SELECT * FROM `users` WHERE `username` = 'alice';

-- Update Step:
UPDATE `users` SET `role` = 'superadmin' WHERE `username` = 'alice';
```

## Explanation

1. `INSERT INTO ... SET` provides a key-value assignment style insertion syntax in MySQL.
2. `TRUNCATE TABLE` drops and recreates the underlying data file structure, resetting identity counters.
