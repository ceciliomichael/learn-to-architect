# Module 07 Exercise Solution

```sql
CREATE TABLE tasks (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  description TEXT NOT NULL,
  completed INTEGER DEFAULT 0
);

INSERT INTO tasks (description) VALUES ('Setup SQLite'), ('Write SQL'), ('Run tests');

-- Safe Update: Step 1 Preview
SELECT * FROM tasks WHERE id = 2;

-- Step 2 Update
UPDATE tasks SET completed = 1 WHERE id = 2;

-- Safe Delete: Step 1 Preview
SELECT * FROM tasks WHERE completed = 1;

-- Step 2 Delete
DELETE FROM tasks WHERE completed = 1;
```

## Explanation

1. `completed INTEGER DEFAULT 0` provides a fallback value of 0.
2. Running `SELECT * FROM tasks WHERE id = 2;` ensures you affect only task 2 during update.
3. Running `SELECT * FROM tasks WHERE completed = 1;` confirms rows targeted for deletion.
