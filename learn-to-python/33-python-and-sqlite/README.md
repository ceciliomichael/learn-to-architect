# Module 33: Use SQLite Safely from Python

## What you will learn

You will open transactions, bind parameters, read named rows, and close connections explicitly.

## Connect to a known path

```python
import sqlite3
from pathlib import Path

database_path = Path("data") / "shop.db"
database_path.parent.mkdir(exist_ok=True)
connection = sqlite3.connect(database_path)
```

Opening a misspelled path can create a new empty database. Resolve and log an appropriate nonsecret path during setup.

Enable required SQLite behavior on every connection:

```python
connection.execute("PRAGMA foreign_keys = ON")
```

## Close and transact separately

The sqlite3 connection context manager commits on success and rolls back on exception, but does not close the connection. Combine it with `closing`:

```python
from contextlib import closing

with closing(sqlite3.connect(database_path)) as connection:
    connection.execute("PRAGMA foreign_keys = ON")
    with connection:
        connection.execute(
            "INSERT INTO products (name, price_cents) VALUES (?, ?)",
            ("Notebook", 425),
        )
```

The inner context controls a transaction. The outer context closes the connection.

## Bind every external value

```python
product_name = input("Product name: ")
row = connection.execute(
    "SELECT product_id, name FROM products WHERE name = ?",
    (product_name,),
).fetchone()
```

The one-item tuple needs its comma. Never use an f-string or concatenation to insert input into SQL. Parameters represent values, not table names, column names, directions, or keywords. Map dynamic identifiers from a fixed allowlist.

## Read named columns

```python
connection.row_factory = sqlite3.Row
row = connection.execute(
    "SELECT product_id, name FROM products WHERE product_id = ?",
    (1,),
).fetchone()
if row is not None:
    print(row["name"])
```

Set the row factory before creating cursors. Rows still need domain validation when the database is not fully trusted.

## Use cursor results intentionally

- `fetchone` returns one row or `None`.
- Iterating the cursor streams rows.
- `fetchall` loads all remaining rows, which may be too large.
- `executemany` runs one parameterized statement for many parameter sets.

Do not share one connection freely across threads. Follow sqlite3's thread-safety reporting, connection options, transaction boundaries, and your application's ownership model.

## Errors and retries

Catch `sqlite3.IntegrityError` only when a known constraint failure can become a domain response. Busy or locked errors need bounded transaction retries when the operation is safe to retry. Do not retry syntax, schema, or programming errors.

## Check your understanding

You are ready when you can show separate transaction and close lifetimes and prove that user values never enter SQL structure.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
