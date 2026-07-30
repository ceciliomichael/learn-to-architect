# Module 05: Create Tables and Understand SQLite Storage Classes

## What You Will Learn

In this module, you will learn how to write `CREATE TABLE` statements, understand SQLite's 5 fundamental storage classes, explore how SQLite handles dynamic type affinity, and discover how to define modern `STRICT` tables for rigid data typing.

---

## SQLite 5 Fundamental Storage Classes

Unlike traditional SQL engines that assign strict types to columns, standard SQLite stores values in one of 5 **storage classes** regardless of column declared type:

1. **`NULL`**: The value is a NULL value.
2. **`INTEGER`**: A signed integer stored in 1, 2, 3, 4, 6, or 8 bytes depending on size.
3. **`REAL`**: A floating point number stored as an 8-byte IEEE floating point number.
4. **`TEXT`**: A text string, stored using database encoding (UTF-8, UTF-16BE, UTF-16LE).
5. **`BLOB`**: A blob of binary data stored exactly as input.

---

## Column Type Affinity vs `STRICT` Tables

### Standard SQLite (Dynamic Type Affinity)
When you define `CREATE TABLE users (age INTEGER);`, SQLite applies **INTEGER type affinity**. It will attempt to convert inserted values (like `'42'`) to an integer, but if you insert `'Forty-Two'`, SQLite will store the string `'Forty-Two'` without throwing an error!

### Modern SQLite `STRICT` Tables
Starting in SQLite 3.37.0+, you can append `STRICT` to the end of a `CREATE TABLE` statement. `STRICT` tables enforce strict type validation and reject values that do not match declared types:

```sql
CREATE TABLE strict_users (
  id INT PRIMARY KEY,
  username TEXT NOT NULL,
  age INT,
  balance REAL
) STRICT;
```

---

## Step-by-Step Practical Example

```sql
-- Standard table (flexible typing)
CREATE TABLE dynamic_demo (
  id INTEGER PRIMARY KEY,
  val INT
);

-- Strict table (rigid typing)
CREATE TABLE strict_demo (
  id INT PRIMARY KEY,
  val INT
) STRICT;

INSERT INTO dynamic_demo VALUES (1, 100), (2, '200'), (3, 'Not A Number');
```

In `dynamic_demo`, all 3 rows succeed. In `strict_demo`, trying to insert `'Not A Number'` into an `INT` column throws an immediate type mismatch error!

---

## Common Beginner Mistakes & Solutions

### 1. Thinking SQLite Has `VARCHAR(255)` Limits
- **Cause**: Coming from MySQL or PostgreSQL where `VARCHAR(255)` limits string length.
- **Fix**: SQLite treats `VARCHAR(n)` simply as `TEXT` affinity. It ignores length parameters unless custom constraints are defined.

---

## Check Your Understanding

1. What are the 5 storage classes in SQLite?
2. How does adding `STRICT` to `CREATE TABLE` change SQLite's behavior?
