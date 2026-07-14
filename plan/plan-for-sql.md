# Plan for the SQL Learning Module

## Purpose

This document tracks the design and implementation of `sql-learning-module/`.

The course is for a learner who has never programmed and has never used a database. It begins with a local SQLite database because SQLite is small, safe to practice with, and does not require a server account. It teaches common relational SQL carefully, labels SQLite-specific behavior, and introduces PostgreSQL only after the learner understands the core language.

The course does not include a miscellaneous module or a final assessment.

## Accuracy foundation

The curriculum is checked against the official SQLite SQL language documentation and the current PostgreSQL documentation.

Important boundaries are stated directly:

1. SQL is a standardized language family, but database products differ in types, functions, schema tools, concurrency, and administrative commands.
2. SQLite uses dynamic typing with column affinity by default. Its `STRICT` tables have a smaller set of accepted type names.
3. The SQLite command-line dot commands, such as `.tables` and `.schema`, are tool commands and are not SQL.
4. `NULL` means missing or unknown information and requires `IS NULL` rather than ordinary equality.
5. Result order is not promised without `ORDER BY`.
6. Data changes must be previewed with a matching `SELECT` and protected with transactions when risk is meaningful.
7. Indexes can speed reads but cost storage and write work. Query plans provide evidence.
8. Parameter binding belongs in the application or database client API. User input must never be joined into SQL text.
9. PostgreSQL roles, schemas, strong types, and isolation behavior are taught as PostgreSQL behavior, not as universal SQL.

## Course promise

Every module will:

- Use only ideas already introduced or explain a new idea before using it
- Keep examples small enough to understand by inspection
- Use plain, friendly language without emoji or em dash characters
- Separate SQL statements from SQLite command-line commands
- Show expected result shapes when that helps a beginner
- Explain why a query works, not only what to type
- Include safe, repeatable exercises
- Include complete exercise solutions and explained quiz answers
- Identify product-specific syntax instead of pretending every database behaves the same

## Required folder structure

Every module will use exactly this learning structure:

```text
module-NN-topic/
  README.md
  exercise/
    exercise.md
  quiz/
    quiz.md
  answers/
    exercise/
      exercise-solutions.md
    quiz/
      quiz-answers.md
```

The module lesson teaches. The exercise file provides guided practice. The quiz checks reasoning. Answer files explain the path to the result.

## Shared practice approach

Exercises use disposable `.db` files. A learner can delete and recreate only a course database when a reset is needed. No exercise uses a production database.

Early modules build a small library database in controlled steps. Later modules create focused databases when isolation makes a concept safer or clearer. Every data-changing module uses this routine:

1. Confirm the database file and table.
2. Start a transaction when appropriate.
3. Preview target rows with `SELECT`.
4. Run the change with a precise condition.
5. Inspect the result.
6. Commit only when correct, otherwise roll back.

## Planned module sequence

### Part 1: Read data with confidence

- [x] **Module 01: Meet Databases, SQL, and SQLite**
  - Database files, tables, rows, columns, SQLite CLI, SQL statements, dot commands, and a safe practice folder.

- [x] **Module 02: Select Columns and Name Results**
  - `SELECT`, `FROM`, explicit columns, `*`, expressions, column aliases, and readable formatting.

- [x] **Module 03: Filter Rows with Comparisons**
  - `WHERE`, equality, inequality, numeric and text comparisons, `BETWEEN`, `IN`, and `LIKE`.

- [x] **Module 04: Understand NULL and Three-Valued Logic**
  - Missing values, `IS NULL`, `IS NOT NULL`, unknown conditions, `COALESCE`, and careful defaults.

- [x] **Module 05: Sort, Remove Duplicates, and Limit Results**
  - `ORDER BY`, multiple sort keys, deterministic ties, `DISTINCT`, `LIMIT`, and `OFFSET` caveats.

- [x] **Module 06: Build Expressions and Decisions**
  - Arithmetic, concatenation, operator order, aliases, searched `CASE`, and avoiding hidden assumptions.

- [x] **Module 07: Use String and Numeric Functions**
  - `length`, `lower`, `upper`, `trim`, `substr`, `round`, `abs`, nested calls, and product differences.

### Part 2: Design and change tables safely

- [x] **Module 08: Create Tables and Choose SQLite Types**
  - `CREATE TABLE`, SQLite storage classes, type affinity, `STRICT`, and portable type expectations.

- [x] **Module 09: Protect Data with Constraints and Keys**
  - `PRIMARY KEY`, `NOT NULL`, `UNIQUE`, `CHECK`, defaults, foreign keys, and constraint failures.

- [x] **Module 10: Insert Rows**
  - Explicit column lists, one and many rows, defaults, generated identifiers, and `RETURNING` as SQLite behavior.

- [x] **Module 11: Update and Delete Rows Safely**
  - Preview-first changes, precise `WHERE`, row counts, all-row changes, and recovery through transactions.

### Part 3: Summarize and connect relational data

- [x] **Module 12: Calculate Aggregate Results**
  - `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, `NULL` behavior, and `COUNT(*)` compared with `COUNT(column)`.

- [x] **Module 13: Group Rows and Filter Groups**
  - `GROUP BY`, one result per group, `HAVING`, grouping rules, and avoiding SQLite's permissive bare columns.

- [x] **Module 14: Join Matching Rows**
  - Primary and foreign key relationships, qualified names, `INNER JOIN`, `ON`, and accidental Cartesian products.

- [x] **Module 15: Keep Unmatched Rows with Outer Joins**
  - `LEFT JOIN`, missing matches, filters in `ON` compared with `WHERE`, self joins, and SQLite right/full support boundaries.

- [x] **Module 16: Model Many-to-Many Relationships**
  - Junction tables, composite keys, multi-table joins, relationship attributes, and preventing duplicates.

### Part 4: Compose larger queries

- [x] **Module 17: Use Subqueries and EXISTS**
  - Scalar, list, and correlated subqueries, `EXISTS`, `NOT EXISTS`, and the `NOT IN` with `NULL` trap.

- [x] **Module 18: Organize Queries with Common Table Expressions**
  - `WITH`, named query steps, multiple CTEs, scope, readability, and planner considerations.

- [x] **Module 19: Combine Result Sets**
  - `UNION`, `UNION ALL`, `INTERSECT`, `EXCEPT`, compatible columns, duplicate handling, and final ordering.

- [x] **Module 20: Design Relational Data and Normalize It**
  - Entities, attributes, functional dependency in plain language, first through third normal form, controlled denormalization, and practical tradeoffs.

### Part 5: Reliability and reusable database behavior

- [x] **Module 21: Use Transactions and Savepoints**
  - Atomic work, `BEGIN`, `COMMIT`, `ROLLBACK`, savepoints, error recovery, and SQLite transaction modes.

- [x] **Module 22: Create and Use Views**
  - Stored queries, stable interfaces, read behavior, view limitations, and careful replacement or migration.

- [x] **Module 23: Create Indexes and Read Query Plans**
  - B-tree indexes, selection and ordering, composite leftmost behavior, unique and partial indexes, write cost, and `EXPLAIN QUERY PLAN`.

### Part 6: Advanced query tools

- [x] **Module 24: Calculate Across Rows with Window Functions**
  - `OVER`, partitions, window ordering, `row_number`, `rank`, `dense_rank`, `lag`, and `lead`.

- [x] **Module 25: Control Window Frames**
  - Running totals, moving calculations, `ROWS`, peers, default frames, and full-partition calculations.

- [x] **Module 26: Work with Dates, Times, and Portability**
  - SQLite time values and functions, ISO 8601 text, Unix time, time zones, intervals as product behavior, and portable storage decisions.

- [x] **Module 27: Walk Hierarchies with Recursive CTEs**
  - Anchor and recursive members, termination, hierarchy depth, path construction, cycles, and recursion safety.

### Part 7: Evolve and automate a schema

- [x] **Module 28: Change Schemas with Migrations**
  - Versioned changes, `ALTER TABLE` limits, table rebuild pattern, data backfills, reversible thinking, backups, and deployment order.

- [x] **Module 29: Upsert, RETURNING, and Generated Values**
  - SQLite `ON CONFLICT`, conflict targets, `excluded`, `RETURNING`, generated columns, and product-specific labeling.

- [x] **Module 30: Use Triggers Carefully**
  - Timing and events, `OLD` and `NEW`, audit examples, recursion risks, hidden behavior, and when application logic is clearer.

### Part 8: Move from local SQL to production database thinking

- [x] **Module 31: Concurrency, Locking, and Isolation**
  - Concurrent transactions, dirty and nonrepeatable reads, phantoms, SQLite locking, PostgreSQL isolation levels, retries, and short transactions.

- [x] **Module 32: PostgreSQL Types, Schemas, and Identity Columns**
  - Strong types, `boolean`, dates, timestamps, numeric precision, UUID, JSONB, schemas, search path, and generated identity.

- [x] **Module 33: Parameterized SQL, Roles, and Least Privilege**
  - SQL injection cause, parameter binding, identifier allowlists, roles, grants, ownership, secrets, and database boundaries.

- [x] **Module 34: Tune Queries with Evidence**
  - Workload definition, representative data, `EXPLAIN` compared with execution, selectivity, statistics, index tradeoffs, query rewrites, measurement, and regression checks.

## Dependency rules

The course must preserve these boundaries:

1. No filter assumes `NULL` behavior before Module 04.
2. No table creation exercise assumes constraints before they are explained.
3. No destructive data change appears before preview-first safety is explained.
4. No aggregation exercise uses grouping until aggregate behavior is established.
5. No join assumes learners already understand keys.
6. No many-to-many query appears before ordinary joins.
7. No CTE appears before subqueries establish nested result thinking.
8. No index claim is accepted without a query plan and realistic workload discussion.
9. No window frame is used before partitions and ordering.
10. No PostgreSQL administrative statement is presented as SQLite or universal SQL.
11. No security example constructs SQL with user-provided text.

## Writing pattern for each lesson

Each `README.md` should normally contain:

1. What you will learn
2. Before you begin
3. A plain-language explanation
4. One small working query at a time
5. Expected rows or result shape
6. Why the query behaves that way
7. Common mistakes
8. Check your understanding
9. A clear connection to the next module

Data-changing and administrative modules also contain a visible safety section.

## Exercise and quiz standard

Exercises should require learners to predict, run, inspect, and explain. Solutions include complete SQL, expected outcomes, and reasoning. Quizzes test understanding rather than punctuation memory, and every answer explains why.

## Estimated focused learning time

The planned course represents about 95 to 150 focused hours:

- Lessons and typed examples: 40 to 60 hours
- Exercises and debugging: 40 to 65 hours
- Quizzes, review, and repeated practice: 15 to 25 hours

The time depends on whether the learner repeats exercises from an empty database and explains results in their own words.

## Implementation checklist

- [x] Confirm the dialect strategy with official SQLite and PostgreSQL documentation
- [x] Define the ordered beginner-to-advanced curriculum
- [x] Create the SQL course root guide
- [x] Create Modules 01 to 07
- [x] Create Modules 08 to 16
- [x] Create Modules 17 to 23
- [x] Create Modules 24 to 30
- [x] Create Modules 31 to 34
- [x] Verify every required folder and file
- [x] Check all relative Markdown links
- [x] Scan for emoji, em dash characters, placeholders, and unbalanced code fences
- [x] Execute representative SQLite lessons in disposable database files
- [x] Update the repository root README
- [x] Mark every roadmap item complete

## Definition of done

The SQL course is complete when all 34 modules exist in the required structure, every concept appears after its prerequisites, SQLite examples execute as written on a current supported SQLite CLI, product-specific behavior is labeled, all answers explain reasoning, all links work, formatting audits pass, and the root README points beginners to the course.
