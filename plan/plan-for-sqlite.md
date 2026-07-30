# Plan for the SQLite Learning Course (`learn-to-sqlite`)

## Purpose

This document tracks the design and implementation of `learn-to-sqlite/`.

`learn-to-sqlite` is a dedicated, zero-to-hero course designed specifically around the SQLite embedded relational database engine. Unlike client-server databases (such as MySQL or PostgreSQL), SQLite runs in-process, reads and writes directly to single disk files, and requires zero background daemon or user management setup.

This course teaches students how SQLite operates under the hood, how to use the `sqlite3` CLI program, how SQLite's dynamic type system works (including `STRICT` tables), PRAGMA commands, transactions, indexing, views, triggers, FTS5 full-text search, JSON storage, and application binding.

---

## Engine Architecture & Core Principles

1. **In-Process & Embedded**: The engine is a C library compiled into your application or CLI tool. There are no sockets, ports, or background server daemons.
2. **File-Based Storage**: The entire database (tables, indexes, triggers, schema) lives inside a single cross-platform file (`.db` or `.sqlite`).
3. **Dynamic Type Affinity vs. STRICT Tables**: By default, SQLite stores values according to dynamic storage classes (`INTEGER`, `REAL`, `TEXT`, `BLOB`, `NULL`) regardless of declared column types. Modern SQLite also supports `STRICT` tables for strict type enforcement.
4. **Dot-Commands vs SQL**: CLI commands (`.headers on`, `.tables`, `.schema`, `.mode box`) configure the shell environment and are **not** SQL statements.
5. **ACID Transactions & WAL**: SQLite supports single-writer ACID transactions using rollback journals or Write-Ahead Logging (`PRAGMA journal_mode=WAL;`).

---

## Course Structure & File Layout Standard

Every module follows the exact repository standard:

```text
learn-to-sqlite/
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

- [x] **Module 01: Meet SQLite, Architecture, and the CLI (`sqlite3`)**
  - Embedded engine concept, opening database files (`library.db`), `.headers`, `.mode box`, `.schema`, `.tables`, `.quit`, running your first query.
- [x] **Module 02: Select Columns and Form Expressions**
  - `SELECT`, `FROM`, column aliases (`AS`), arithmetic expressions, string concatenation (`||`), handling quote escaping.
- [x] **Module 03: Filter Rows and Master Three-Valued Logic (`NULL`)**
  - `WHERE`, comparisons (`=`, `!=`, `<`, `>`), `BETWEEN`, `IN`, `LIKE`, `IS NULL`, `IS NOT NULL`, `COALESCE`.
- [x] **Module 04: Sort, Remove Duplicates, and Limit Results**
  - `ORDER BY`, `ASC`/`DESC`, multiple sort keys, `DISTINCT`, `LIMIT`, and `OFFSET`.
- [x] **Module 05: Create Tables and Understand SQLite Storage Classes**
  - `CREATE TABLE`, 5 storage classes (`NULL`, `INTEGER`, `REAL`, `TEXT`, `BLOB`), type affinity, and `STRICT` table definitions.
- [x] **Module 06: Protect Data with Constraints and Configure PRAGMAs**
  - `PRIMARY KEY`, `AUTOINCREMENT`, `NOT NULL`, `UNIQUE`, `CHECK`, `FOREIGN KEY`, `PRAGMA foreign_keys = ON;`.
- [x] **Module 07: Insert, Update, and Delete Data Safely**
  - Previewing changes with `SELECT`, single/multi-row `INSERT`, `UPDATE ... WHERE`, `DELETE ... WHERE`, safe practices.
- [x] **Module 08: Group and Aggregate Data**
  - `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, `GROUP BY`, `HAVING`, `COUNT(*)` vs `COUNT(column)`.
- [x] **Module 09: Connect Data with Joins**
  - `INNER JOIN`, `LEFT JOIN`, `CROSS JOIN`, table aliases, joining multiple tables.
- [x] **Module 10: Compose Queries with Subqueries and CTEs**
  - Scalar subqueries, list subqueries, `EXISTS` / `NOT EXISTS`, `WITH` clause Common Table Expressions.
- [x] **Module 11: Manage Transactions and Savepoints**
  - `BEGIN TRANSACTION`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`, concurrency locks, WAL mode (`PRAGMA journal_mode=WAL;`).
- [x] **Module 12: Speed Up Queries with Indexes and Analyze Execution**
  - B-Trees, single and composite indexes, `EXPLAIN QUERY PLAN`, avoiding unnecessary indexes.
- [x] **Module 13: Store Reusable Queries with Views and Automate with Triggers**
  - `CREATE VIEW`, read-only queries, `CREATE TRIGGER`, `BEFORE`/`AFTER`, `NEW` and `OLD` records, auditing.
- [x] **Module 14: Compute Across Rows with Window Functions**
  - `OVER()`, `PARTITION BY`, `ORDER BY`, `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `LAG()`, `LEAD()`, window frames.
- [x] **Module 15: Full-Text Search (FTS5), JSON, and Application Integration**
  - `FTS5` virtual tables, `MATCH` operator, JSON functions (`json_extract`, `json_object`), connecting SQLite to Python/Node.js.

---

## Definition of Done

1. All 15 modules fully created with no placeholders or truncated code.
2. Complete exercise instructions, quiz questions, exercise solutions, and quiz answer explanations in every module.
3. Explicit line-by-line breakdowns for code and queries.
