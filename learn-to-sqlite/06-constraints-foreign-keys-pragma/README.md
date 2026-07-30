# Module 06: Protect Data with Constraints and Configure PRAGMAs

## What You Will Learn

In this module, you will learn how to enforce domain rules using `PRIMARY KEY`, `AUTOINCREMENT`, `NOT NULL`, `UNIQUE`, `CHECK`, foreign keys, and how to enable foreign key enforcement in SQLite using `PRAGMA foreign_keys = ON;`.

---

## Data Integrity Constraints

Constraints prevent invalid data from entering your tables:

- **`PRIMARY KEY`**: Uniquely identifies each record.
- **`AUTOINCREMENT`**: Prevents SQLite from reusing primary key IDs of deleted rows.
- **`NOT NULL`**: Ensures a field cannot be NULL.
- **`UNIQUE`**: Prevents duplicate values across rows.
- **`CHECK (condition)`**: Enforces custom boolean logic for inserted/updated rows.
- **`FOREIGN KEY`**: Establishes parent-child table relationships.

---

## Important SQLite Quirks: Foreign Keys & PRAGMAs

By default, for backward compatibility, SQLite **disables foreign key enforcement**.

To enforce foreign key relationships, you **must** run this command in every database session:

```sql
PRAGMA foreign_keys = ON;
```

---

## Step-by-Step Practical Example

```sql
PRAGMA foreign_keys = ON;

CREATE TABLE departments (
  dept_id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL UNIQUE
);

CREATE TABLE employees (
  emp_id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  salary REAL CHECK(salary > 0),
  dept_id INTEGER NOT NULL,
  FOREIGN KEY (dept_id) REFERENCES departments(dept_id) ON DELETE CASCADE
);

INSERT INTO departments (name) VALUES ('Engineering'), ('Marketing');

INSERT INTO employees (name, salary, dept_id) VALUES 
  ('Alice', 95000.0, 1),
  ('Bob', 82000.0, 2);
```

If you try to insert an employee with `dept_id = 999`, SQLite rejects the write:
`Runtime error: FOREIGN KEY constraint failed`.

---

## Check Your Understanding

1. Why must `PRAGMA foreign_keys = ON;` be executed in your SQLite session?
2. What does `CHECK(salary > 0)` enforce?
