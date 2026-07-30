# Quiz Answers: Meet Databases, SQL, and SQLite

1. One book record.
2. A column defines one specific attribute/fact stored for every record in the table.
3. No. `.tables` is a SQLite CLI dot command used to configure or query the terminal tool environment. Dot commands do not end in semicolons and are specific to the SQLite CLI program. SQL statements (like `SELECT`) interact with the database engine itself and end with semicolons.
4. A semicolon (`;`).
5. Every column from every row currently stored in the `books` table.
6. In the local `library.db` file opened on disk.
7. SQLite is an **embedded** engine that reads/writes a single local file without running a server process. MySQL and PostgreSQL are **client-server** engines running as background daemons (`mysqld` or `postgres`) that handle client network connections, user accounts, and concurrent write throughput.
8. Modules 01–25 focus on core ANSI SQL logic using SQLite. Modules 26–34 transition to dialect differences, concurrency, role permissions, and production tuning in client-server databases like PostgreSQL and MySQL.

