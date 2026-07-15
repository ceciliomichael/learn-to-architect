# Exercise Solutions: Use SQLite Safely from Python

```python
from contextlib import closing
from pathlib import Path
import sqlite3

path = Path("sqlite-practice.db")
with closing(sqlite3.connect(path)) as connection:
    connection.row_factory = sqlite3.Row
    connection.execute("PRAGMA foreign_keys = ON")
    with connection:
        connection.execute(
            """
            CREATE TABLE IF NOT EXISTS products (
                product_id INTEGER PRIMARY KEY,
                name TEXT NOT NULL UNIQUE,
                price_cents INTEGER NOT NULL CHECK (price_cents >= 0)
            ) STRICT
            """
        )
        connection.executemany(
            "INSERT INTO products (name, price_cents) VALUES (?, ?)",
            [("Pen", 125), ("Pad", 350), ("Book", 1200)],
        )

    wanted = "Pad"
    row = connection.execute(
        "SELECT product_id, name, price_cents FROM products WHERE name = ?",
        (wanted,),
    ).fetchone()
    if row is not None:
        print(row["name"], row["price_cents"])

    for row in connection.execute(
        "SELECT product_id, name FROM products ORDER BY product_id"
    ):
        print(row["product_id"], row["name"])

    try:
        with connection:
            connection.execute(
                "INSERT INTO products (name, price_cents) VALUES (?, ?)",
                ("Pen", 200),
            )
    except sqlite3.IntegrityError:
        print("A product with that name already exists.")

    count = connection.execute(
        "SELECT COUNT(*) FROM products WHERE name = ?",
        ("Pen",),
    ).fetchone()[0]
    print("Pen rows after rollback:", count)
```

The final count is one, so the failed duplicate did not add a partial row. The connection remains usable until `closing` exits. The transaction context commits successful work or rolls back failed work, while `closing` handles the separate responsibility of closing the connection.
