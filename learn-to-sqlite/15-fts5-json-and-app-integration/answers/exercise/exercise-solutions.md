# Module 15 Exercise Solution

```sql
CREATE VIRTUAL TABLE articles USING fts5(heading, content);

INSERT INTO articles VALUES 
  ('Intro to SQLite', 'Learn how SQLite runs in process.'),
  ('Advanced Database Concepts', 'Comparing indexing strategies.');

SELECT * FROM articles WHERE articles MATCH 'SQLite';

-- JSON Extraction:
CREATE TABLE settings (id INT PRIMARY KEY, config TEXT);
INSERT INTO settings VALUES (1, '{"status": "active", "theme": "dark"}');

SELECT id FROM settings WHERE json_extract(config, '$.status') = 'active';
```

### Expected Output

```text
┌─────────────────┬──────────────────────────────────┐
│     heading     │             content              │
├─────────────────┼──────────────────────────────────┤
│ Intro to SQLite │ Learn how SQLite runs in process.│
└─────────────────┴──────────────────────────────────┘
```

## Explanation

1. `fts5` virtual table indexing enables fast text matching with `MATCH`.
2. `json_extract(config, '$.status')` parses JSON string data dynamically.
