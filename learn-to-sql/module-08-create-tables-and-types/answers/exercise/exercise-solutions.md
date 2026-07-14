# Exercise Solutions: Create Tables and Choose SQLite Types

## Exercise 1

```sql
SELECT
  typeof(7) AS integer_type,
  typeof(7.5) AS real_type,
  typeof('7') AS text_type,
  typeof(NULL) AS null_type,
  typeof(X'4142') AS blob_type;
```

The result is `integer`, `real`, `text`, `null`, and `blob`.

## Exercise 2

```sql
CREATE TABLE measurements (
  measurement_id INTEGER,
  label TEXT,
  value REAL,
  raw_data BLOB
) STRICT;
```

Then run `.schema measurements`.

## Exercise 3

```sql
INSERT INTO measurements
  (measurement_id, label, value, raw_data)
VALUES
  (1, 'room', 21.5, X'4142');

INSERT INTO measurements
  (measurement_id, label, value, raw_data)
VALUES
  (2, 'package', 'heavy', X'4344');
```

The second statement fails because `heavy` cannot be losslessly stored as `REAL` in a strict table. Verify:

```sql
SELECT * FROM measurements;
```
