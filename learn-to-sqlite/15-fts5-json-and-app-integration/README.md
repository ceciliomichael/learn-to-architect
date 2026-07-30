# Module 15: Full-Text Search (FTS5), JSON, and Application Integration

## What You Will Learn

In this module, you will learn how to leverage SQLite's `FTS5` extension for fast full-text searching, store and extract structured JSON documents (`json_extract`, `json_object`), and connect SQLite database files to Python or Node.js application backends.

---

## Full-Text Search with `FTS5`

`FTS5` is a virtual table module built into SQLite designed for rapid full-text text searches using the `MATCH` operator.

```sql
CREATE VIRTUAL TABLE documents USING fts5(title, body);

INSERT INTO documents VALUES
  ('SQLite Architecture', 'SQLite is an in-process embedded database library.'),
  ('MySQL Guide', 'MySQL is a client-server relational database daemon.');

-- Search documents matching 'embedded'
SELECT * FROM documents WHERE documents MATCH 'embedded';
```

---

## Working with JSON Data

SQLite includes native JSON functions for manipulating JSON text:

- `json_extract(json_text, '$.path')`: Extracts a value at a specified path.
- `json_object('key', value)`: Constructs a JSON string object.

```sql
CREATE TABLE user_profiles (
  id INTEGER PRIMARY KEY,
  attributes TEXT -- JSON string
);

INSERT INTO user_profiles VALUES (1, '{"theme": "dark", "notifications": true}');

SELECT id, json_extract(attributes, '$.theme') AS theme
FROM user_profiles
WHERE json_extract(attributes, '$.notifications') = true;
```

---

## Application Integration Example (Python `sqlite3`)

SQLite is embedded into Python's standard library:

```python
import sqlite3

# Connect to database file
conn = sqlite3.connect("practice.db")
cursor = conn.cursor()

# Parameterized query (prevents SQL injection)
cursor.execute("SELECT name, salary FROM employees WHERE salary > ?", (50000,))
rows = cursor.fetchall()

for name, salary in rows:
    print(f"Employee: {name}, Salary: ${salary:,.2f}")

conn.close()
```

---

## Check Your Understanding

1. Why are parameters (`?`) used in application code instead of string concatenation?
2. How does an `FTS5` virtual table differ from a standard table?
