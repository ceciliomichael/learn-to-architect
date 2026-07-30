# Plan for the MySQL Learning Course (`learn-to-mysql`)

## Purpose

This document tracks the design and implementation of `learn-to-mysql/`.

`learn-to-mysql` is a dedicated, zero-to-hero course designed specifically around MySQL / MariaDB client-server relational database management systems. Unlike embedded file-based engines (such as SQLite), MySQL runs as a separate server process daemon (`mysqld`), listens on network ports (typically `3306`), and enforces client authentication, user privileges, strict data types, storage engines (InnoDB), and multi-user concurrency control.

This course teaches students how client-server database architectures operate, how to use the `mysql` CLI client and connection parameters, MySQL-specific data types (`VARCHAR`, `DATETIME`, `DECIMAL`, `ENUM`), `AUTO_INCREMENT`, InnoDB locking & isolation levels, stored procedures, triggers, views, user privileges (`GRANT`/`REVOKE`), `mysqldump` backups, and performance tuning using `EXPLAIN FORMAT=TREE`.

---

## Engine Architecture & Core Principles

1. **Client-Server Model**: The database engine runs as a server daemon (`mysqld`). Applications connect over network sockets using credentials (host, port, username, password).
2. **Strict Data Types**: MySQL enforces strict column types (`INT`, `VARCHAR(n)`, `DECIMAL(p,s)`, `DATETIME`). Dynamic type coercion is strictly governed by `sql_mode`.
3. **Storage Engines**: Pluggable storage architecture. Modern MySQL defaults to `InnoDB` (ACID compliant, row-level locking, foreign key constraints, crash recovery).
4. **Auto-Increment & Identity**: Primary key surrogate IDs use `INT AUTO_INCREMENT PRIMARY KEY`.
5. **Multi-User Security & Privilege Model**: Access is managed through user accounts (`username@host`) with granular database, table, and command permissions.

---

## Course Structure & File Layout Standard

Every module follows the repository standard:

```text
learn-to-mysql/
├── README.md
├── module-directory/
│   ├── README.md
│   ├── exercise/
│   │   └── exercise.md
│   ├── quiz/
│   │   └── quiz.md
│   └── answers/
│       ├── exercise/
│       │   └── exercise-solutions.md
│       └── quiz/
│           └── quiz-answers.md
```

---

## Planned Module Sequence

- [x] **Module 01: Meet MySQL, Client-Server Architecture, and the `mysql` CLI**
  - Daemon process (`mysqld`), TCP port 3306, client connections (`mysql -u user -p -h host`), databases vs schemas, `SHOW DATABASES;`, `USE db_name;`, `SHOW TABLES;`.
- [x] **Module 02: Select Columns, Expressions, and Column Aliases**
  - `SELECT`, `FROM`, backtick identifier quoting (`` `col` ``), string concatenation with `CONCAT()`, aliases (`AS`).
- [x] **Module 03: Filter Rows, Operators, and Handling `NULL`**
  - `WHERE`, comparison operators, `LIKE` / `NOT LIKE`, `IN`, `BETWEEN`, `IS NULL`, `IS NOT NULL`, `IFNULL()`, `COALESCE()`.
- [x] **Module 04: Sort, Limit, and Paginate Large Result Sets**
  - `ORDER BY`, `ASC`/`DESC`, `DISTINCT`, `LIMIT count OFFSET offset`, pagination formulas for web applications.
- [x] **Module 05: Master MySQL Data Types and Table Creation**
  - `CREATE TABLE`, `INT`, `BIGINT`, `VARCHAR(n)`, `TEXT`, `DECIMAL(p,s)`, `DATE`, `DATETIME`, `TIMESTAMP`, `ENUM`, strict `sql_mode`.
- [x] **Module 06: Protect Data with Constraints and `AUTO_INCREMENT`**
  - `PRIMARY KEY`, `INT AUTO_INCREMENT`, `NOT NULL`, `UNIQUE`, `DEFAULT`, `FOREIGN KEY ... REFERENCES ... ON DELETE CASCADE`.
- [x] **Module 07: Insert, Update, and Delete Data with Multi-Row Syntax**
  - `INSERT INTO ... VALUES (...)`, `INSERT INTO ... SET`, `UPDATE ... WHERE`, `DELETE FROM ... WHERE`, `TRUNCATE TABLE`.
- [x] **Module 08: Group and Aggregate Data**
  - `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`, `GROUP BY`, `HAVING`, strict `ONLY_FULL_GROUP_BY` enforcement.
- [x] **Module 09: Join Tables and Model Relational Schema**
  - `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `CROSS JOIN`, composite foreign keys, junction tables for many-to-many relationships.
- [x] **Module 10: Compose Queries with Subqueries and CTEs**
  - Subqueries in `WHERE`/`FROM`, `EXISTS` / `NOT EXISTS`, Common Table Expressions (`WITH ... AS ()`).
- [x] **Module 11: Storage Engines (InnoDB), Locking, and Transaction Control**
  - InnoDB vs MyISAM, `START TRANSACTION`, `COMMIT`, `ROLLBACK`, transaction isolation levels (`READ COMMITTED`, `REPEATABLE READ`), row-level locks.
- [x] **Module 12: Speed Up Queries with Indexes and Execution Trees**
  - B-Tree primary & secondary indexes, composite indexes, `EXPLAIN`, `EXPLAIN FORMAT=TREE`, index cardinality.
- [x] **Module 13: Views, Stored Procedures, and Triggers**
  - `CREATE VIEW`, `DELIMITER //`, `CREATE PROCEDURE`, IN/OUT parameters, `CREATE TRIGGER` (`BEFORE INSERT`, `AFTER UPDATE`).
- [x] **Module 14: Window Functions and Native JSON Data Handling**
  - `OVER (PARTITION BY ... ORDER BY ...)`, `ROW_NUMBER()`, `RANK()`, `JSON` column type, `JSON_EXTRACT()`, `->`, `->>`.
- [x] **Module 15: User Privilege Management, Security, and Backups**
  - `CREATE USER`, `GRANT ALL PRIVILEGES / SELECT ON`, `REVOKE`, `FLUSH PRIVILEGES;`, backup and restore with `mysqldump`.

---

## Definition of Done

1. All 15 modules fully created with no placeholders or truncated code.
2. Complete exercise instructions, quiz questions, exercise solutions, and quiz answer explanations in every module.
3. Explicit line-by-line breakdowns for code and queries.
