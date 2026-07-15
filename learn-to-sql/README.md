# SQL Learning Module

This course teaches SQL from the beginning. You do not need programming experience or database experience.

You will begin with SQLite, a database that stores everything in a local file and needs no server account. Most early query skills transfer to other relational databases. When SQLite and PostgreSQL behave differently, the lesson says so clearly.

## How to use this course

Complete the modules in order. Every module contains:

1. A lesson in `README.md`
2. Guided work in `exercise/exercise.md`
3. A short quiz in `quiz/quiz.md`
4. Worked exercise solutions in `answers/exercise/exercise-solutions.md`
5. Explained quiz answers in `answers/quiz/quiz-answers.md`

Type each SQL statement yourself. Predict the result before pressing Enter, then compare your prediction with the actual rows.

## Two ways to run the examples

### Option 1: Use an online environment

Online environments like [DB Fiddle](https://www.db-fiddle.com/) or [SQLite Online](https://sqliteonline.com/) run in a web browser and require no setup. This is the simplest choice for the first few modules.

### Option 2: Work on your computer

Install a current SQLite command-line program from <https://www.sqlite.org/download.html>.

Open a terminal and check the installation:

```text
sqlite3 --version
```

The examples use SQLite 3.35 or newer. A current version is recommended. Advanced PostgreSQL modules explain when a PostgreSQL installation is useful, but you do not need it for the beginner path.

## Course path

### Part 1: Read data with confidence

- [Module 01: Meet Databases, SQL, and SQLite](01-meet-databases-sqlite/README.md)
- [Module 02: Select Columns and Name Results](02-select-columns/README.md)
- [Module 03: Filter Rows with Comparisons](03-filter-with-comparisons/README.md)
- [Module 04: Understand NULL and Three-Valued Logic](04-null-and-three-valued-logic/README.md)
- [Module 05: Sort, Remove Duplicates, and Limit Results](05-sort-distinct-and-limit/README.md)
- [Module 06: Build Expressions and Decisions](06-expressions-and-case/README.md)
- [Module 07: Use String and Numeric Functions](07-string-and-numeric-functions/README.md)

### Part 2: Design and change tables safely

- [Module 08: Create Tables and Choose SQLite Types](08-create-tables-and-types/README.md)
- [Module 09: Protect Data with Constraints and Keys](09-constraints-and-keys/README.md)
- [Module 10: Insert Rows](10-insert-rows/README.md)
- [Module 11: Update and Delete Rows Safely](11-update-and-delete-safely/README.md)

### Part 3: Summarize and connect relational data

- [Module 12: Calculate Aggregate Results](12-aggregate-results/README.md)
- [Module 13: Group Rows and Filter Groups](13-group-by-and-having/README.md)
- [Module 14: Join Matching Rows](14-inner-joins/README.md)
- [Module 15: Keep Unmatched Rows with Outer Joins](15-outer-and-self-joins/README.md)
- [Module 16: Model Many-to-Many Relationships](16-many-to-many-relationships/README.md)

### Part 4: Compose larger queries

- [Module 17: Use Subqueries and EXISTS](17-subqueries-and-exists/README.md)
- [Module 18: Organize Queries with Common Table Expressions](18-common-table-expressions/README.md)
- [Module 19: Combine Result Sets](19-set-operations/README.md)
- [Module 20: Design Relational Data and Normalize It](20-normalization/README.md)

### Part 5: Reliability and reusable database behavior

- [Module 21: Use Transactions and Savepoints](21-transactions-and-savepoints/README.md)
- [Module 22: Create and Use Views](22-views/README.md)
- [Module 23: Create Indexes and Read Query Plans](23-indexes-and-query-plans/README.md)

### Part 6: Advanced query tools

- [Module 24: Calculate Across Rows with Window Functions](24-window-functions/README.md)
- [Module 25: Control Window Frames](25-window-frames/README.md)
- [Module 26: Work with Dates, Times, and Portability](26-dates-times-and-portability/README.md)
- [Module 27: Walk Hierarchies with Recursive CTEs](27-recursive-ctes/README.md)

### Part 7: Evolve and automate a schema

- [Module 28: Change Schemas with Migrations](28-schema-migrations/README.md)
- [Module 29: Upsert, RETURNING, and Generated Values](29-upsert-returning-and-generated-values/README.md)
- [Module 30: Use Triggers Carefully](30-triggers/README.md)

### Part 8: Production database thinking

- [Module 31: Concurrency, Locking, and Isolation](31-concurrency-and-isolation/README.md)
- [Module 32: PostgreSQL Types, Schemas, and Identity Columns](32-postgresql-types-and-schemas/README.md)
- [Module 33: Parameterized SQL, Roles, and Least Privilege](33-parameterized-sql-and-roles/README.md)
- [Module 34: Tune Queries with Evidence](34-query-tuning/README.md)

## Safety rule for the whole course

Only practice in disposable course database files. Before an `UPDATE` or `DELETE`, run a `SELECT` with the same condition. Use a transaction when a mistake could affect several rows. Never practice on a workplace, school, or production database without explicit permission and a reviewed plan.
