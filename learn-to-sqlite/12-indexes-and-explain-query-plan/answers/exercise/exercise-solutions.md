# Module 12 Exercise Solution

```sql
CREATE TABLE logs (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  status_code INTEGER,
  ip_address TEXT
);

-- Before Index:
EXPLAIN QUERY PLAN SELECT * FROM logs WHERE status_code = 404;
-- Output: SCAN logs

-- Create Index:
CREATE INDEX idx_logs_status ON logs(status_code);

-- After Index:
EXPLAIN QUERY PLAN SELECT * FROM logs WHERE status_code = 404;
-- Output: SEARCH logs USING INDEX idx_logs_status (status_code=?)
```

## Explanation

1. `SCAN logs` indicates an inefficient sequential read across all rows.
2. `SEARCH logs USING INDEX` indicates that SQLite uses the B-Tree index to jump straight to status code 404.
