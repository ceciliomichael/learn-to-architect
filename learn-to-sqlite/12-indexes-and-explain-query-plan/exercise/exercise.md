# Module 12 Exercise

1. Create table `logs` (`id` INT PRIMARY KEY, `status_code` INT, `ip_address` TEXT).
2. Write `EXPLAIN QUERY PLAN SELECT * FROM logs WHERE status_code = 404;` and note the output.
3. Create an index `idx_logs_status` on `status_code`.
4. Re-run `EXPLAIN QUERY PLAN` and verify that SQLite now performs a `SEARCH TABLE`.
