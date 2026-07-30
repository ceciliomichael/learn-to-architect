# Module 12 Exercise Solution

```sql
-- Step 1: Before Index
EXPLAIN FORMAT=TREE SELECT * FROM `users` WHERE `email` = 'bob@example.com';
-- Output: -> Table scan on users

-- Step 2: Create Index
CREATE INDEX `idx_users_email` ON `users`(`email`);

-- Step 3: After Index
EXPLAIN FORMAT=TREE SELECT * FROM `users` WHERE `email` = 'bob@example.com';
-- Output: -> Index lookup on users using idx_users_email (email='bob@example.com')
```

## Explanation

1. Without an index, MySQL performs a full sequential table scan.
2. The index allows MySQL to perform an $O(\log N)$ B-Tree lookup.
