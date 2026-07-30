# Module 01 Quiz: SQLite CLI & Architecture Fundamentals

## Questions

1. Which of the following best describes SQLite's architecture?
   - A) A client application that connects to a `mysqld` background service over port 3306.
   - B) An embedded C library that reads and writes directly to a single disk file without a server daemon.
   - C) A distributed cloud database requiring network authentication and user grants.
   - D) A web browser extension for visualizing SQL tables.

2. What is the purpose of the dot-command `.headers on` in the SQLite CLI?
   - A) It adds primary key headers to your table schema.
   - B) It instructs the SQLite engine to generate HTTP header responses.
   - C) It tells the CLI terminal to display column names at the top of query results.
   - D) It enforces strict data typing across all string columns.

3. Why did the command `SELECT 1 + 1` fail to execute when the user pressed Enter?
   - A) SQLite cannot calculate arithmetic expressions without a `FROM` clause.
   - B) The statement was missing a terminating semicolon `;`.
   - C) The user did not specify double quotes around the numbers.
   - D) The database file was not locked in WAL mode.
