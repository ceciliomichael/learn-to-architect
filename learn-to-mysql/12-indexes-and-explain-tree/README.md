# Module 12: Speed Up Queries with Indexes and Execution Trees

## What You Will Learn

In this module, you will learn how B-Tree indexes operate in MySQL, create single and composite indexes (`CREATE INDEX`), inspect execution plans with `EXPLAIN` and `EXPLAIN FORMAT=TREE` (MySQL 8.0+), and optimize query execution.

---

## Creating Indexes in MySQL

```sql
-- Single Column B-Tree Index
CREATE INDEX `idx_users_email` ON `users`(`email`);

-- Composite (Multi-Column) Index
CREATE INDEX `idx_orders_customer_date` ON `orders`(`customer_id`, `created_at`);
```

### Prefix Indexes for Strings
For long `VARCHAR` or `TEXT` fields, create a prefix index on the first $N$ characters:
```sql
CREATE INDEX `idx_users_bio_prefix` ON `users`(`bio`(20));
```

---

## Performance Inspection: `EXPLAIN FORMAT=TREE`

Prefix any `SELECT` query with `EXPLAIN FORMAT=TREE` in MySQL 8.0+ to print a clear visual execution plan tree:

```sql
EXPLAIN FORMAT=TREE SELECT * FROM `users` WHERE `email` = 'alice@example.com';
```

### Output Example
```text
EXPLAIN
-> Index lookup on users using idx_users_email (email='alice@example.com')  (cost=0.35 rows=1)
```

If it reads `-> Table scan on users`, MySQL is scanning all rows sequentially.

---

## Check Your Understanding

1. What command formats MySQL execution plans as a hierarchical tree in MySQL 8.0+?
2. What is the Leftmost Prefix Rule in composite indexes?
