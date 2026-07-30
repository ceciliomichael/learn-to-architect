# Module 07: Insert, Update, and Delete Data Safely

## What You Will Learn

In this module, you will learn how to add rows with `INSERT`, modify existing records with `UPDATE`, remove rows with `DELETE`, and enforce the critical **preview-first workflow** to prevent accidental data loss.

---

## The `INSERT` Statement

To insert new rows, specify target table, explicit column names, and row values:

```sql
INSERT INTO members (name, email, level) VALUES
  ('Alice Vance', 'alice@example.com', 'Gold'),
  ('Bob Smith', 'bob@example.com', 'Silver');
```

---

## The `UPDATE` Statement (With Safety Routine)

`UPDATE` modifies values in existing rows matching a `WHERE` condition.

```sql
UPDATE members SET level = 'Platinum' WHERE name = 'Alice Vance';
```

### The Safety Protocol
Before running an `UPDATE`, **always run a preview `SELECT`** with the exact same `WHERE` condition!

```sql
-- STEP 1: Preview target rows
SELECT * FROM members WHERE name = 'Alice Vance';

-- STEP 2: Execute UPDATE
UPDATE members SET level = 'Platinum' WHERE name = 'Alice Vance';

-- STEP 3: Verify results
SELECT * FROM members WHERE name = 'Alice Vance';
```

---

## The `DELETE` Statement

`DELETE` removes rows matching a condition:

```sql
-- STEP 1: Preview rows to be deleted
SELECT * FROM members WHERE level = 'Silver';

-- STEP 2: Delete rows
DELETE FROM members WHERE level = 'Silver';
```

---

## Check Your Understanding

1. What happens if you execute `UPDATE members SET level = 'Gold';` without a `WHERE` clause?
2. Why should you run a `SELECT` query prior to running `DELETE`?
