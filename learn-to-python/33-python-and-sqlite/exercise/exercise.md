# Exercises: Use SQLite Safely from Python

1. Create a disposable database and strict products table.
2. Insert several rows with executemany and bound parameters in one transaction.
3. Query by a user-provided name with a parameter.
4. Use sqlite3.Row and stream ordered results.
5. Trigger a unique constraint, convert only that expected IntegrityError to a clear message, and prove rollback behavior.
