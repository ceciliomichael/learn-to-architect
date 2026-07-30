# Module 06 Exercise

1. Enable foreign key support using `PRAGMA foreign_keys = ON;`.
2. Create a parent table `authors` (`author_id` PRIMARY KEY, `name` UNIQUE).
3. Create a child table `books` (`book_id` PRIMARY KEY, `title` NOT NULL, `author_id` FOREIGN KEY).
4. Attempt to insert a book referencing a non-existent `author_id` to verify constraint rejection.
