# Module 06 Exercise Solution

```sql
PRAGMA foreign_keys = ON;

CREATE TABLE authors (
  author_id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL UNIQUE
);

CREATE TABLE books (
  book_id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT NOT NULL,
  author_id INTEGER NOT NULL,
  FOREIGN KEY (author_id) REFERENCES authors(author_id)
);

INSERT INTO authors (name) VALUES ('Jane Austen');

-- Invalid insert (throws foreign key constraint failure)
INSERT INTO books (title, author_id) VALUES ('Unknown Masterpiece', 99);
```

## Explanation

1. `PRAGMA foreign_keys = ON;` activates foreign key checks.
2. Inserting `author_id = 99` fails because `99` does not exist in `authors`.
