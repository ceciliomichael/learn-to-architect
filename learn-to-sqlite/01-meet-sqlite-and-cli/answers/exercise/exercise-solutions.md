# Module 01 Exercise Solution

## Terminal Commands & SQL

```bash
mkdir sqlite_mod01_practice
cd sqlite_mod01_practice
sqlite3 test_db.sqlite
```

Inside the SQLite prompt:

```text
.headers on
.mode box
```

```sql
SELECT 'Learn SQLite' AS course_name, 1 AS module_number;
```

### Expected Output

```text
┌──────────────┬───────────────┐
│ course_name  │ module_number │
├──────────────┼───────────────┤
│ Learn SQLite │ 1             │
└──────────────┴───────────────┘
```

Exit the CLI:

```text
.databases
.quit
```

## Explanation

1. `sqlite3 test_db.sqlite` initializes the file `test_db.sqlite`.
2. `.headers on` and `.mode box` format CLI output tables cleanly with border lines.
3. `SELECT 'Learn SQLite' AS course_name, 1 AS module_number;` calculates two literal values, assigns column aliases using `AS`, and terminates with a semicolon `;`.
4. `.databases` displays the absolute file path of `test_db.sqlite`, confirming persistence, and `.quit` exits cleanly.
