# Learn MySQL Step by Step (`learn-to-mysql`)

Welcome to **Learn MySQL Step by Step**!

MySQL is one of the world's most popular open-source relational database management systems (RDBMS). It powers leading web applications, enterprise platforms, content management systems (like WordPress and Drupal), and modern cloud infrastructure (AWS RDS, GCP Cloud SQL, Azure Database for MySQL).

Unlike embedded file databases (such as SQLite), MySQL runs as a dedicated **server process daemon** (`mysqld`), listens on network ports (typically port `3306`), enforces strict user account privileges, uses pluggable storage engines (like InnoDB), and handles high concurrent read/write traffic.

---

## Why Learn MySQL?

1. **Client-Server Production Architecture**: Master connecting to live database daemons, managing network host permissions, ports, sockets, and server connection pools.
2. **Enterprise Concurrency & Security**: Understand InnoDB row-level locking, ACID multi-user isolation levels, grant privileges (`GRANT`/`REVOKE`), and SSL/TLS network transport security.
3. **Strict Data Type Enforcement**: Learn how MySQL manages `VARCHAR`, `INT`, `DECIMAL`, `DATETIME`, `TIMESTAMP`, `ENUM`, and strict `sql_mode` settings.
4. **Production Tooling & Optimization**: Build hands-on expertise with `mysql` CLI, `mysqldump` backups, stored procedures, triggers, views, and `EXPLAIN FORMAT=TREE` performance profiling.

---

## Course Roadmap (15 Modules)

### Part 1: Architecture, Connections, and Basic Queries
- [Module 01: Meet MySQL, Client-Server Architecture, and the `mysql` CLI](./01-meet-mysql-architecture-and-client/README.md)
- [Module 02: Select Columns, Expressions, and Column Aliases](./02-select-and-column-aliases/README.md)
- [Module 03: Filter Rows, Operators, and Handling `NULL`](./03-filtering-nulls-and-operators/README.md)
- [Module 04: Sort, Limit, and Paginate Large Result Sets](./04-sorting-limiting-and-pagination/README.md)

### Part 2: Table Creation, Data Types, and Data Changes
- [Module 05: Master MySQL Data Types and Table Creation](./05-mysql-data-types-and-tables/README.md)
- [Module 06: Protect Data with Constraints and `AUTO_INCREMENT`](./06-constraints-foreign-keys-auto-increment/README.md)
- [Module 07: Insert, Update, and Delete Data with Multi-Row Syntax](./07-insert-update-delete-transactions/README.md)

### Part 3: Aggregates, Relationships, and Subqueries
- [Module 08: Group and Aggregate Data](./08-aggregates-and-grouping/README.md)
- [Module 09: Join Tables and Model Relational Schema](./09-table-joins-and-relationships/README.md)
- [Module 10: Compose Queries with Subqueries and CTEs](./10-subqueries-and-ctes/README.md)

### Part 4: Storage Engines, Indexing, and Enterprise Features
- [Module 11: Storage Engines (InnoDB), Locking, and Transaction Control](./11-storage-engines-innodb-and-locking/README.md)
- [Module 12: Speed Up Queries with Indexes and Execution Trees](./12-indexes-and-explain-tree/README.md)
- [Module 13: Views, Stored Procedures, and Triggers](./13-views-stored-procedures-triggers/README.md)
- [Module 14: Window Functions and Native JSON Data Handling](./14-window-functions-and-json/README.md)
- [Module 15: User Privilege Management, Security, and Backups](./15-user-management-security-and-backups/README.md)

---

## Module Structure

Every module contains 5 essential parts:
1. `README.md` - Comprehensive conceptual guide with step-by-step terminal commands and line-by-line breakdowns.
2. `exercise/exercise.md` - Hands-on practice tasks.
3. `quiz/quiz.md` - Conceptual review questions.
4. `answers/exercise/exercise-solutions.md` - Full SQL solution statements with explanations.
5. `answers/quiz/quiz-answers.md` - Detailed quiz answer key and explanations.
