# Module 05: Master MySQL Data Types and Table Creation

## What You Will Learn

In this module, you will learn how to write `CREATE TABLE` statements in MySQL, choose appropriate strict column data types (`INT`, `VARCHAR(n)`, `DECIMAL(p,s)`, `DATETIME`, `ENUM`), understand character sets and collations (`utf8mb4`), and understand strict `sql_mode` enforcement.

---

## Core MySQL Data Types

Unlike SQLite's dynamic type affinity, MySQL strictly enforces column data types:

| Type Family | Specific Types | Use Cases & Description |
| :--- | :--- | :--- |
| **Numeric** | `TINYINT`, `INT`, `BIGINT`, `DECIMAL(precision, scale)` | `INT` for primary keys, `DECIMAL(10,2)` for exact monetary values without floating-point errors. |
| **String** | `VARCHAR(length)`, `TEXT`, `ENUM('a', 'b')` | `VARCHAR(255)` for variable text up to length limits; `ENUM` restricts column values to fixed list strings. |
| **Date & Time** | `DATE`, `TIME`, `DATETIME`, `TIMESTAMP` | `DATE` (`YYYY-MM-DD`), `DATETIME` (`YYYY-MM-DD HH:MM:SS`), `TIMESTAMP` (auto-converts UTC). |

---

## Character Sets and Collations (`utf8mb4`)

When creating MySQL tables, specify `utf8mb4` (4-byte UTF-8) to support full Unicode (including emojis):

```sql
CREATE TABLE `users` (
  `id` INT AUTO_INCREMENT PRIMARY KEY,
  `username` VARCHAR(50) NOT NULL UNIQUE,
  `bio` TEXT,
  `role` ENUM('admin', 'editor', 'user') DEFAULT 'user',
  `created_at` DATETIME DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```

---

## Strict SQL Modes (`sql_mode`)

MySQL uses `sql_mode` flags (e.g. `STRICT_TRANS_TABLES`, `ONLY_FULL_GROUP_BY`). Under strict modes, inserting out-of-range or invalid data throws an error immediately rather than saving truncated data with warnings.

---

## Check Your Understanding

1. Why should `DECIMAL(10,2)` be used for currency values instead of `FLOAT` or `DOUBLE`?
2. What character set choice guarantees complete Unicode (emoji) support in MySQL?
