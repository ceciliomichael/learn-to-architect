# Exercise Solutions: Meet Databases, SQL, and SQLite

## Exercise 1

Outside SQLite:

```text
sqlite3 --version
mkdir sql-course-practice
cd sql-course-practice
sqlite3 library.db
```

Inside SQLite:

```text
.headers on
.mode box
.databases
```

The database list should show a `main` entry ending in `library.db`.

## Exercise 2

Run the exact `CREATE TABLE` and `INSERT` statements from the lesson. Between them, inspect:

```text
.tables
.schema books
```

`books` should appear. The schema output should contain six column definitions.

### Schema Explanation:
- `book_id INTEGER PRIMARY KEY`: Unique numeric identifier for each row.
- `title TEXT NOT NULL`: Title string; cannot be missing/empty.
- `published_year INTEGER`: Year published; can be `NULL` (missing/unknown).

## Exercise 3

```sql
SELECT * FROM books;
```

The result should contain book identifiers 1 through 6. Then:

```text
.quit
sqlite3 library.db
```

Turn headers and box mode on again because these are CLI session settings:

```text
.headers on
.mode box
SELECT * FROM books;
```

The rows remain because they were saved permanently in `library.db`.

### Engine Behavior Explanation:
ANSI SQL standard queries like `SELECT * FROM books;` use standard SQL syntax understood by SQLite, MySQL, and PostgreSQL alike. Learning SQL query logic in SQLite directly applies when querying MySQL or PostgreSQL tables in production.

