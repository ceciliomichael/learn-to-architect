# Learn SQLite Step by Step (`learn-to-sqlite`)

Welcome to **Learn SQLite Step by Step**!

SQLite is the most widely deployed database engine in the world. It powers mobile applications on iOS and Android, desktop software, embedded devices, edge computing platforms, and local developer workflows.

Unlike server-based database systems like MySQL or PostgreSQL, SQLite is an **embedded database library**. It runs inside your application or CLI process and writes directly to a single disk file. It requires zero server configuration, zero background daemons, and zero user authentication setup.

---

## Why Learn SQLite?

1. **Zero Setup Friction**: Open a terminal, type `sqlite3 mydata.db`, and you immediately have a production-grade relational database running in a local file.
2. **Universal SQL Standard**: SQLite implements most of the standard ANSI SQL specification. The query skills you learn here (`SELECT`, `WHERE`, `JOIN`, `GROUP BY`, subqueries, CTEs, window functions) transfer directly to PostgreSQL, MySQL, SQL Server, and Oracle.
3. **Embedded Architecture**: Understand how applications interact with local file-backed storage, Write-Ahead Logging (WAL), and single-writer ACID transactions.
4. **Rich Advanced Features**: Includes `STRICT` tables, PRAGMA tuning options, Full-Text Search (FTS5), JSON storage, recursive queries, and triggers.

---

## Course Roadmap (15 Modules)

### Part 1: Core Queries and CLI Mastery
- [Module 01: Meet SQLite, Architecture, and the CLI (`sqlite3`)](./01-meet-sqlite-and-cli/README.md)
- [Module 02: Select Columns and Form Expressions](./02-select-columns-and-expressions/README.md)
- [Module 03: Filter Rows and Master Three-Valued Logic (`NULL`)](./03-filtering-and-nulls/README.md)
- [Module 04: Sort, Remove Duplicates, and Limit Results](./04-sorting-distinct-and-limit/README.md)

### Part 2: Table Design, Types, and Data Manipulation
- [Module 05: Create Tables and Understand SQLite Storage Classes](./05-creating-tables-and-storage-classes/README.md)
- [Module 06: Protect Data with Constraints and Configure PRAGMAs](./06-constraints-foreign-keys-pragma/README.md)
- [Module 07: Insert, Update, and Delete Data Safely](./07-insert-update-delete/README.md)

### Part 3: Aggregation, Joins, and Subqueries
- [Module 08: Group and Aggregate Data](./08-aggregates-and-group-by/README.md)
- [Module 09: Connect Data with Joins](./09-table-joins/README.md)
- [Module 10: Compose Queries with Subqueries and CTEs](./10-subqueries-and-ctes/README.md)

### Part 4: Transactions, Indexing, and Advanced Features
- [Module 11: Manage Transactions and Savepoints](./11-transactions-and-savepoints/README.md)
- [Module 12: Speed Up Queries with Indexes and Analyze Execution](./12-indexes-and-explain-query-plan/README.md)
- [Module 13: Store Reusable Queries with Views and Automate with Triggers](./13-views-and-triggers/README.md)
- [Module 14: Compute Across Rows with Window Functions](./14-window-functions-and-frames/README.md)
- [Module 15: Full-Text Search (FTS5), JSON, and Application Integration](./15-fts5-json-and-app-integration/README.md)

---

## Module Structure

Every module contains 5 essential parts:
1. `README.md` - In-depth conceptual guide with step-by-step terminal examples and line-by-line breakdowns.
2. `exercise/exercise.md` - Hands-on practice tasks.
3. `quiz/quiz.md` - Conceptual review questions.
4. `answers/exercise/exercise-solutions.md` - Full SQL solution statements with explanations.
5. `answers/quiz/quiz-answers.md` - Detailed quiz answer key and explanations.
