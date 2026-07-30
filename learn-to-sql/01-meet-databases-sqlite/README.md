# Module 01: Meet Databases, SQL, and SQLite

## What you will learn

You will understand what a database is, open SQLite, create a disposable database file, run your first SQL statements with line-by-line explanations of what is happening, and understand how SQLite compares to client-server engines like MySQL and PostgreSQL.

---

## What is happening under the hood?

When you work with a database, three main pieces interact:

```text
+-----------------------+      +------------------------+      +------------------------+
|  Terminal / CLI Tool  | ---> |   Database Engine      | ---> | Database File on Disk  |
|  (e.g., sqlite3 CLI)  |      | (Interprets your SQL)  |      |   (e.g., library.db)   |
+-----------------------+      +------------------------+      +------------------------+
```

1. **The CLI Tool (`sqlite3`)**: Accepts your commands from the keyboard.
2. **The Database Engine**: Reads your SQL statement, checks it for correctness, executes the logic, and formats the output.
3. **The Database File (`library.db`)**: Stores your tables, columns, and rows permanently on disk.

---

## SQL vs. CLI Commands (Dot Commands)

In SQLite, you will use two different types of commands:

| Command Type | Example | Ends With Semicolon? | Purpose | Standard Across MySQL/PostgreSQL? |
| :--- | :--- | :--- | :--- | :--- |
| **Dot Command (CLI settings)** | `.headers on`, `.mode box` | **No** | Configures the terminal display or CLI tool environment. | No (SQLite CLI specific) |
| **SQL Statement (Data query)** | `SELECT * FROM books;` | **Yes (`;)** | Instructs the database engine to define, retrieve, or alter data. | **Yes** (ANSI SQL standard) |

---

## Database Engine Context: SQLite vs. MySQL & PostgreSQL

Beginners often ask: *Why start with SQLite instead of MySQL or PostgreSQL? When will I use MySQL? How do I choose between them?*

Here is the exact distinction and course roadmap:

- **SQLite (`learn-to-sqlite`)**: An embedded database library. It stores your database inside a single local file on your computer (`library.db`). There is no background server process running, no port to open, and no user account setup needed. It is ideal for local desktop software, mobile applications (iOS/Android), and mastering SQL query logic without setup friction.
- **MySQL (`learn-to-mysql`)**: A client-server database engine. A background server daemon (`mysqld`) runs continuously listening on network port `3306`. Applications connect over the network using hostnames, ports, usernames, and passwords. It is built for multi-user web applications, concurrent production traffic, and granular user security privileges.

### Clear Transition Roadmap

1. **`learn-to-sql` (This Course)**: Teaches universal ANSI SQL logic (`SELECT`, `WHERE`, `JOIN`, `GROUP BY`, `HAVING`, subqueries, CTEs, views, indexes) using SQLite for instant, zero-friction execution.
2. **`learn-to-sqlite`**: Dedicated course for deep SQLite mastery (PRAGMAs, `STRICT` tables, FTS5 full-text search, WAL mode, application embedding).
3. **`learn-to-mysql`**: Dedicated course for client-server production database engineering (`mysqld`, port 3306, user grants, InnoDB locking, `AUTO_INCREMENT`, stored procedures, `mysqldump`).

---

## Step 1: Open a safe database file

Create a dedicated practice folder on your computer and launch SQLite:

```text
mkdir sql-course-practice
cd sql-course-practice
sqlite3 library.db
```

### What just happened?
- `sqlite3 library.db` asks the SQLite CLI program to open `library.db`.
- If `library.db` does not exist yet, SQLite creates a new, blank file on disk.
- You are now at the interactive SQLite prompt: `sqlite>`.

Now format the terminal output so columns align clearly in box tables:

```text
.headers on
.mode box
```

- `.headers on`: Tells the CLI tool to print column names at the top of results.
- `.mode box`: Displays query results formatted inside visual clean box borders.

---

## Step 2: Run your first SQL statement

At the `sqlite>` prompt, type:

```sql
SELECT 'Hello, SQL!' AS message;
```

### Output:
```text
┌──────────────┐
│   message    │
├──────────────┤
│ Hello, SQL!  │
└──────────────┘
```

### Line-by-line breakdown of what happened:
- `SELECT`: The SQL keyword asking the engine to calculate or retrieve a result.
- `'Hello, SQL!'`: A text literal string enclosed in single quotes.
- `AS message`: Names the resulting column `message` (an alias).
- `;`: **The semicolon ends the SQL statement.** The database engine does not execute your command until it sees a semicolon!

---

## Step 3: Create a table (`CREATE TABLE`)

A relational database table holds structured records organized in columns and rows. Run this statement to create a table named `books`:

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

### Line-by-line breakdown of what each line means:

- `CREATE TABLE books`: Instructs the engine to create a new table named `books`.
- `book_id INTEGER PRIMARY KEY`: Defines column `book_id`. `INTEGER` means numbers without decimals. `PRIMARY KEY` guarantees each row has a unique identifier number.
- `title TEXT NOT NULL`: Defines column `title`. `TEXT` means text strings. `NOT NULL` prevents saving a book without a title.
- `author TEXT NOT NULL`: Defines column `author` as required text.
- `published_year INTEGER`: Defines column `published_year`. Notice it does NOT have `NOT NULL`, meaning the year can be omitted (`NULL`).
- `price REAL NOT NULL`: Defines column `price`. `REAL` stores floating-point numbers with decimal points (e.g., `24.50`).
- `in_stock INTEGER NOT NULL`: Defines column `in_stock`. SQLite uses `1` for true (in stock) and `0` for false (out of stock).

---

## Step 4: Add practice rows (`INSERT INTO`)

Now populate the `books` table with six rows of data:

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

### What happened under the hood?
- `INSERT INTO books (...)`: Specifies the table and the target column order.
- `VALUES (...)`: Each set of parentheses contains the values for one row, separated by commas.
- `NULL` (in row 4): Indicates that the published year for *Web Basics* is unknown or missing.
- The engine checks each row against your constraints (e.g., verifying `book_id` is unique and required columns are not empty) and writes all six rows into `library.db`.

---

## Step 5: Read the whole table (`SELECT *`)

To verify your data was written successfully, query the table:

```sql
SELECT * FROM books;
```

### Output:
```text
┌─────────┬────────────────────┬─────────────┬────────────────┬───────┬──────────┐
│ book_id │       title        │   author    │ published_year │ price │ in_stock │
├─────────┼────────────────────┼─────────────┼────────────────┼───────┼──────────┤
│ 1       │ First Steps in SQL │ Mira Chen   │ 2021           │ 24.5  │ 1        │
│ 2       │ Quiet Algorithms   │ Tomas Reed  │ 2019           │ 31.0  │ 0        │
│ 3       │ Practical Databases│ Mira Chen   │ 2023           │ 28.75 │ 1        │
│ 4       │ Web Basics         │ Lena Ortiz  │                │ 19.99 │ 1        │
│ 5       │ Data Stories       │ Omar Nasser │ 2020           │ 22.0  │ 0        │
│ 6       │ Type Safe Programs │ Lena Ortiz  │ 2024           │ 35.5  │ 1        │
└─────────┴────────────────────┴─────────────┴────────────────┴───────┴──────────┘
```

- `*`: An asterisk means "select all columns".
- `FROM books`: Specifies the table to read from.

---

## Step 6: Inspect and save your session

Use SQLite dot commands to inspect your database metadata:

```text
.tables
.schema books
.databases
```

- `.tables`: Lists all tables in the current database (`books`).
- `.schema books`: Prints the exact `CREATE TABLE` SQL code used to build `books`.
- `.databases`: Shows the file path of your open database file (`library.db`).

Exit SQLite safely:

```text
.quit
```

Your data is safely stored in `library.db`. If you open SQLite again with `sqlite3 library.db` and run `SELECT * FROM books;`, all your data will still be there!

---

## Common Beginner Mistakes & Fixes

### 1. The prompt shows `...> ` and nothing happens
- **Cause**: You forgot the semicolon `;` at the end of your SQL statement.
- **Fix**: Type `;` and press Enter.

### 2. `Error: no such table: books`
- **Cause**: You opened SQLite from a different folder or misspelled the file name.
- **Fix**: Run `.databases` to verify which file is open, or exit with `.quit` and ensure you are in `sql-course-practice`.

### 3. Using double quotes for text strings (e.g., `"Mira Chen"`)
- **Cause**: In SQL, double quotes are for column or table names with spaces, while single quotes `'Mira Chen'` are for literal text values.
- **Fix**: Always use single quotes `'...'` for text data values.

---

## Check your understanding

You are ready when you can:
1. Explain the difference between CLI dot commands (`.mode`) and SQL queries (`SELECT`).
2. Describe what `PRIMARY KEY`, `NOT NULL`, and `NULL` mean in a table definition.
3. Re-open `library.db` from your terminal and verify that your data persists.
4. Explain why we start with SQLite and how standard SQL transfers to MySQL and PostgreSQL.

---

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

