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

## Exercise 3

```sql
SELECT * FROM books;
```

The result should contain book identifiers 1 through 6. Then:

```text
.quit
sqlite3 library.db
```

Turn headers and box mode on again because these are CLI session settings, then repeat the query. The rows remain because they were stored in the database file.
