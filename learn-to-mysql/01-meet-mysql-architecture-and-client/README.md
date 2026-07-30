# Module 01: Meet MySQL, Client-Server Architecture, and the `mysql` CLI

## What You Will Learn

In this module, you will understand the client-server architecture of MySQL, how the server daemon (`mysqld`) operates on TCP port 3306, how to connect using the `mysql` CLI client tool, inspect available databases, select active databases, and execute your first MySQL query.

---

## Client-Server Architecture

Unlike embedded file databases (such as SQLite), MySQL uses a **client-server architecture**:

```text
+-----------------------+                         +-------------------------+
|     MySQL Client      |   TCP/IP Port 3306      |   MySQL Server Daemon   |
| (mysql CLI / App code) | ---------------------> |        (mysqld)         |
+-----------------------+                         +-------------------------+
                                                              |
                                                              v
                                                    +-------------------------+
                                                    | InnoDB Storage Engine   |
                                                    +-------------------------+
```

1. **The Server Daemon (`mysqld`)**: Runs continuously as a service, manages data files, buffers memory, handles locking, and enforces security permissions.
2. **Network Protocol**: Listens on TCP port `3306` (or Unix domain sockets).
3. **The Client Tool (`mysql`)**: Command-line executable used by developers and administrators to pass connection parameters and SQL statements to the server.

---

## Connecting to MySQL with `mysql` CLI

To connect to a running MySQL instance from your terminal:

```bash
mysql -u root -p -h 127.0.0.1 -P 3306
```

### Connection Flags Breakdown:
- `-u root`: Specifies the user account (`root`).
- `-p`: Prompts securely for the password.
- `-h 127.0.0.1`: Connects to host (localhost IP).
- `-P 3306`: Specifies target TCP port.

---

## Inspecting Databases & Navigating MySQL

Once connected, your prompt changes to `mysql>`.

```sql
-- 1. List available databases on the server
SHOW DATABASES;

-- 2. Create a disposable course database
CREATE DATABASE company_db;

-- 3. Select active database for your session
USE company_db;

-- 4. Check active database
SELECT DATABASE();
```

---

## Running Your First MySQL Query

At the `mysql>` prompt:

```sql
SELECT 'Welcome to MySQL!' AS greeting, VERSION() AS mysql_version;
```

### Output

```text
+-------------------+---------------+
| greeting          | mysql_version |
+-------------------+---------------+
| Welcome to MySQL! | 8.0.36        |
+-------------------+---------------+
```

### Line-by-Line Breakdown
- `SELECT`: SQL command to evaluate and return expressions.
- `'Welcome to MySQL!' AS greeting`: String literal aliased as column `greeting`.
- `VERSION() AS mysql_version`: Built-in MySQL server function returning the exact server engine version string.
- `;`: Semicolon terminates the statement.

---

## Common Beginner Mistakes & Solutions

### 1. `ERROR 1046 (3D000): No database selected`
- **Cause**: Trying to query or create tables without running `USE database_name;` first.
- **Fix**: Run `USE company_db;` before creating or selecting tables.

---

## Check Your Understanding

1. What process executes database operations in MySQL?
2. What default TCP port does `mysqld` listen on?
3. What statement changes your active working database in the `mysql` CLI?
