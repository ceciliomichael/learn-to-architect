# Module 02: Select Columns and Form Expressions

## What You Will Learn

In this module, you will learn how to read specific columns from tables, alias result columns using `AS`, perform calculations within `SELECT` statements, concatenate string fields using the `||` operator, and avoid common syntax traps.

---

## The Anatomy of a `SELECT` Query

The `SELECT` statement retrieves rows and columns from one or more database tables.

```sql
SELECT column1, column2 FROM table_name;
```

If you want to view every column in a table without listing them explicitly, you can use the asterisk wildcard (`*`):

```sql
SELECT * FROM table_name;
```

---

## Expressions & Column Aliases (`AS`)

You can perform calculations directly inside your `SELECT` list. By default, SQLite names the result column after the expression itself. You can assign a clear human-readable column name using `AS`:

```sql
SELECT title, price, price * 1.08 AS price_with_tax FROM products;
```

### String Concatenation (`||`)

In SQLite, strings are joined together using the double-pipe operator (`||`):

```sql
SELECT first_name || ' ' || last_name AS full_name FROM employees;
```

---

## Step-by-Step Practical Example

Let's open SQLite and create a temporary table to query:

```bash
sqlite3 bookstore.db
```

```sql
.headers on
.mode box

CREATE TABLE items (
  item_id INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  price REAL NOT NULL,
  quantity INTEGER NOT NULL
);

INSERT INTO items (item_id, name, price, quantity) VALUES
  (1, 'Notebook', 4.50, 10),
  (2, 'Fountain Pen', 12.00, 5);

SELECT 
  name, 
  price, 
  quantity, 
  price * quantity AS total_value 
FROM items;
```

### Output

```text
┌──────────────┬───────┬──────────┬─────────────┐
│     name     │ price │ quantity │ total_value │
├──────────────┼───────┼──────────┼─────────────┤
│ Notebook     │ 4.5   │ 10       │ 45.0        │
│ Fountain Pen │ 12.0  │ 5        │ 60.0        │
└──────────────┴───────┴──────────┴─────────────┘
```

---

## Line-by-Line Breakdown

- `SELECT name, price, quantity`: Requests the three stored columns from the table.
- `, price * quantity AS total_value`: Computes a new dynamic value by multiplying `price` and `quantity` for each row, naming the resulting output column `total_value`.
- `FROM items;`: Identifies `items` as the source table.

---

## Check Your Understanding

1. How do you combine two text fields into a single column in SQLite?
2. What is the purpose of the `AS` keyword in a query?
