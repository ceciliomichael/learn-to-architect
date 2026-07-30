# Module 07: Insert, Update, and Delete Data with Multi-Row Syntax

## What You Will Learn

In this module, you will learn how to write multi-row `INSERT` statements, use `INSERT INTO ... SET` syntax, perform safe preview-first `UPDATE` and `DELETE` queries, and understand the difference between `DELETE FROM table` and `TRUNCATE TABLE`.

---

## Multi-Row `INSERT` in MySQL

```sql
INSERT INTO `users` (`username`, `email`, `role`) VALUES
  ('alice', 'alice@example.com', 'admin'),
  ('bob', 'bob@example.com', 'user'),
  ('charlie', 'charlie@example.com', 'editor');
```

### MySQL-Specific `INSERT ... SET` Syntax
```sql
INSERT INTO `users` 
SET `username` = 'diana', `email` = 'diana@example.com', `role` = 'user';
```

---

## Safe `UPDATE` & `DELETE` (Preview-First Protocol)

Always run a preview `SELECT` before mutating rows:

```sql
-- STEP 1: Preview rows to update
SELECT * FROM `users` WHERE `role` = 'editor';

-- STEP 2: Execute update
UPDATE `users` SET `role` = 'admin' WHERE `role` = 'editor';
```

---

## `DELETE FROM` vs `TRUNCATE TABLE`

- `DELETE FROM table WHERE ...`: Deletes matching rows one by one, firing row-level triggers and allowing rollback inside a transaction.
- `TRUNCATE TABLE table`: DDL statement that drops and recreates the table instantly. It resets `AUTO_INCREMENT` back to 1 and cannot be rolled back!

---

## Check Your Understanding

1. What is the key functional difference between `DELETE FROM table;` and `TRUNCATE TABLE table;`?
2. How does `INSERT INTO ... SET` syntax work in MySQL?
