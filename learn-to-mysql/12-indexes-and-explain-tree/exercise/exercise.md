# Module 12 Exercise

1. Run `EXPLAIN FORMAT=TREE SELECT * FROM users WHERE email = 'bob@example.com';`.
2. Create an index `idx_users_email` on `users(email)`.
3. Re-run `EXPLAIN FORMAT=TREE` and verify that the plan changes from Table Scan to Index Lookup.
