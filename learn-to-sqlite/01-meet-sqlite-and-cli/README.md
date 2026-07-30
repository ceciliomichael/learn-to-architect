# Module 01: Meet SQLite, Architecture, and the CLI (`sqlite3`)

## What You Will Learn

In this module, you will understand what SQLite is, how its embedded file-based architecture differs from client-server database systems, how to open or create a local database file, run CLI dot-commands, and execute your first standard SQL query with line-by-line breakdown explanations.

---

## What is SQLite?

SQLite is a C-language library that implements a self-contained, serverless, zero-configuration, transactional SQL database engine.

Unlike client-server databases like MySQL or PostgreSQL, where your application connects over a network socket to a background daemon (`mysqld` or `postgres`), SQLite runs **directly inside your application process**.

```text
CLIENT-SERVER ARCHITECTURE (MySQL / PostgreSQL):
[ Application ] ---> (Network Socket / Port 3306) ---> [ Server Daemon ] ---> [ Storage Files ]

EMBEDDED ARCHITECTURE (SQLite):
[ Application + SQLite Library ] ---------------------> [ Single File on Disk (e.g. app.db) ]
```

### Key Differences at a Glance

| Feature / Aspect | SQLite | MySQL / Client-Server |
| :--- | :--- | :--- |
| **Architecture** | In-process embedded library | Server daemon running on a port |
| **Setup Overhead** | Zero setup (just point to a file) | Install server, configure port/users |
| **Storage** | Single file on disk (cross-platform) | Internal server directory structure |
| **Network Configuration** | None | Host IP, Port, Username, Password |
| **Primary Use Cases** | Mobile apps, desktop apps, local dev, edge | Multi-user web apps, enterprise scale |

---

## Step 1: Open or Create a Safe Practice Database File

Open your terminal, navigate to a disposable practice directory, and launch `sqlite3` passing a database filename:

```bash
mkdir sqlite-practice
cd sqlite-practice
sqlite3 practice.db
```

### What Just Happened?
1. The `sqlite3` program launches.
2. It looks for a file named `practice.db` in the current folder.
3. If `practice.db` does not exist yet, SQLite creates a new 0-byte file on disk.
4. You are presented with the interactive prompt: `sqlite>`.

---

## Step 2: SQL Statements vs. CLI Dot-Commands

SQLite interactive mode uses two distinct kinds of input:

1. **Dot-Commands**: Commands that start with a period (`.`). These configure the CLI interface or query database metadata. They are **not** SQL and must **not** end with a semicolon.
2. **SQL Statements**: Standard database commands. They **must** end with a semicolon (`;`).

Let's configure the CLI display for readable output:

```text
.headers on
.mode box
```

- `.headers on`: Prints column names above query result rows.
- `.mode box`: Encloses table output in visual box borders.

---

## Step 3: Run Your First SQL Query

At the `sqlite>` prompt, enter the following statement:

```sql
SELECT 'Welcome to SQLite!' AS greeting, 2026 AS current_year;
```

### Expected Output

```text
┌────────────────────┬──────────────┐
│      greeting      │ current_year │
├────────────────────┼──────────────┤
│ Welcome to SQLite! │ 2026         │
└────────────────────┴──────────────┘
```

### Line-by-Line Breakdown

- `SELECT`: The SQL keyword used to request data or compute expressions.
- `'Welcome to SQLite!'`: A string literal enclosed in single quotes.
- `AS greeting`: Gives the result column the display name `greeting` (a column alias).
- `,`: Separates expressions in the `SELECT` list.
- `2026 AS current_year`: Computes the number `2026` and aliases the column as `current_year`.
- `;`: **Crucial Semicolon.** Tells SQLite that the SQL statement is complete and ready to execute.

---

## Step 4: Inspect Schema and Exit Safely

To inspect your database file metadata using CLI dot-commands:

- `.tables`: Lists all tables in the current database file.
- `.schema`: Displays the `CREATE TABLE` definitions for existing tables.
- `.databases`: Shows the file path associated with the open database.
- `.quit`: Exits the SQLite CLI tool safely.

---

## Common Beginner Mistakes & Solutions

### 1. The Prompt Shows `...> ` and Nothing Happens
- **Cause**: You forgot to include the semicolon `;` at the end of your SQL statement.
- **Fix**: Type `;` and press Enter.

### 2. Double Quotes vs. Single Quotes
- **Cause**: Writing `"Welcome"` instead of `'Welcome'`.
- **Fix**: In standard SQL, single quotes (`'...'`) define string values, while double quotes (`"..."`) are reserved for table and column names.

---

## Check Your Understanding

1. What is the fundamental difference between an embedded database (SQLite) and a client-server database (MySQL)?
2. Why does a dot-command like `.mode box` not end with a semicolon?
3. What happens if you type a multi-line query in `sqlite3` without adding `;`?
