# Exercises: Meet Databases, SQL, and SQLite

## Exercise 1: Check and open SQLite

1. Check the SQLite version outside the SQLite prompt using `sqlite3 --version`.
2. Create and enter directory `sql-course-practice`.
3. Open database file `library.db`.
4. Turn headers on (`.headers on`) and use box mode (`.mode box`).
5. Ask `.databases` which file is open and verify it points to `library.db`.

## Exercise 2: Create the library and understand the schema

1. Run the complete `CREATE TABLE books` statement from the lesson.
2. Ask `.tables` whether `books` exists.
3. Ask `.schema books` to view the SQL statement that defined `books`.
4. Run the complete six-row `INSERT INTO books` statement from the lesson.
5. Explain what `INTEGER PRIMARY KEY`, `TEXT NOT NULL`, and `NULL` mean in this schema.

## Exercise 3: Read, persist, and understand engine behavior

1. Select every column and row from `books` using `SELECT * FROM books;`.
2. Confirm there are six visible rows formatted in box mode.
3. Quit SQLite with `.quit`.
4. Reopen `library.db` and select all rows again to prove data persists in the file.
5. Explain why standard SQL queries like `SELECT * FROM books;` work the same way in SQLite, MySQL, and PostgreSQL.

