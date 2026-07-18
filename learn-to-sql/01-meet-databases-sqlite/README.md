# Module 01: Meet Databases, SQL, and SQLite

## What you will learn

You will understand tables, open SQLite, create a disposable database, and run your first SQL statement.

## What a relational database stores

A database is an organized collection of data. A relational database usually organizes related facts into tables.

A table has:

- Columns that describe which facts are stored
- Rows that represent individual records
- A name so a query can refer to it

For a library, one row can represent one book. Columns can hold its identifier, title, author, year, price, and stock state.

SQL is a language for defining, reading, changing, and protecting relational data. SQL is not one database product. SQLite and PostgreSQL both understand SQL, but each also has its own behavior and extra features.

## Open a safe database file

Create and enter a folder named `sql-course-practice`. Then run:

```text
sqlite3 library.db
```

SQLite creates `library.db` if it does not exist and opens an interactive prompt. The file is your disposable practice database.

Make results easier to read:

```text
.headers on
.mode box
```

Commands beginning with a dot belong to the SQLite command-line program. They are not SQL and do not end with semicolons.

## Run your first SQL statement

At the SQLite prompt, type:

```sql
SELECT 'Hello, SQL!' AS message;
```

`SELECT` asks for a result. The quoted text is a text value. `AS message` names the result column. The semicolon ends the SQL statement.

SQL keywords are written in uppercase in this course so they are easy to see. SQLite does not require uppercase keywords.

## Create the course table

The following setup creates one table. Type it as one statement:

```sql
CREATE TABLE books (
  book_id INTEGER PRIMARY KEY,
  title TEXT NOT NULL,
  author TEXT NOT NULL,
  published_year INTEGER,
  price REAL NOT NULL,
  in_stock INTEGER NOT NULL
);
```

For now, read it this way:

- `CREATE TABLE books` makes a table named `books`.
- Each following line defines one column.
- `INTEGER`, `TEXT`, and `REAL` describe expected kinds of values.
- `PRIMARY KEY` makes `book_id` the unique row identifier.
- `NOT NULL` says a value is required.

Modules 08 and 09 teach every detail. Here, the statement is a complete setup recipe and the list above gives enough meaning to use it honestly.

## Add the practice rows

```sql
INSERT INTO books
  (book_id, title, author, published_year, price, in_stock)
VALUES
  (1, 'First Steps in SQL', 'Mira Chen', 2021, 24.50, 1),
  (2, 'Quiet Algorithms', 'Tomas Reed', 2019, 31.00, 0),
  (3, 'Practical Databases', 'Mira Chen', 2023, 28.75, 1),
  (4, 'Web Basics', 'Lena Ortiz', NULL, 19.99, 1),
  (5, 'Data Stories', 'Omar Nasser', 2020, 22.00, 0),
  (6, 'Type Safe Programs', 'Lena Ortiz', 2024, 35.50, 1);
```

`INSERT INTO` names the table and columns. Each parenthesized list after `VALUES` becomes one row. Text uses single quotes. `NULL` represents missing or unknown information and is taught carefully in Module 04. This data uses `1` for in stock and `0` for not in stock.

## Read the whole table

```sql
SELECT * FROM books;
```

`*` asks for all columns. `FROM books` names the source table. You should see six rows.

## Inspect without changing data

Useful SQLite tool commands are:

```text
.tables
.schema books
.databases
```

- `.tables` lists tables.
- `.schema books` shows the statement that created the table.
- `.databases` shows the open database file.

Leave SQLite with:

```text
.quit
```

Your data remains in `library.db`.

## Common mistakes

### Forgetting the semicolon

SQLite waits for the rest of the SQL statement. Add `;` and press Enter.

### Using double quotes for text

Use single quotes for text values. Double quotes are intended for identifiers such as unusual table or column names.

### Opening a different file later

Check `.databases`. Similar empty database files are easy to create from the wrong folder.

## Check your understanding

You are ready when you can explain a table, row, and column, distinguish a dot command from SQL, and reopen `library.db` to see the six books.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
