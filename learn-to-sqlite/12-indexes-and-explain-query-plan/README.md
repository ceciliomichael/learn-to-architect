# Module 12: Speed Up Queries with Indexes and Analyze Execution

## What You Will Learn

In this module, you will learn how B-Tree indexes speed up lookups, create single and composite indexes, use `EXPLAIN QUERY PLAN` to verify whether queries use a full table scan (`SCAN TABLE`) or index lookup (`SEARCH TABLE`), and balance read performance against write overhead.

---

## What is an Index?

An index is a separate data structure (typically a B-Tree) that stores sorted keys alongside pointers to table rows.

- Without an index: SQLite performs a **Full Table Scan** (`SCAN TABLE`), reading every single row on disk sequentially (`O(N)` complexity).
- With an index: SQLite performs a **Binary B-Tree Search** (`SEARCH TABLE`), locating target rows rapidly in `O(log N)` time.

```sql
CREATE INDEX idx_users_email ON users(email);
```

### Composite Indexes
```sql
CREATE INDEX idx_orders_cust_date ON orders(customer_id, order_date);
```

---

## Analyzing Performance with `EXPLAIN QUERY PLAN`

Prefix any query with `EXPLAIN QUERY PLAN` to inspect SQLite's query plan:

```sql
EXPLAIN QUERY PLAN SELECT * FROM users WHERE email = 'alice@example.com';
```

### Output Example
```text
QUERY PLAN
`--SEARCH users USING INDEX idx_users_email (email=?)
```

If it reads `SCAN TABLE users`, SQLite is scanning all rows sequentially.

---

## Check Your Understanding

1. What is the write cost associated with creating indexes on frequently updated tables?
2. What does `SEARCH TABLE ... USING INDEX` signify in `EXPLAIN QUERY PLAN`?
