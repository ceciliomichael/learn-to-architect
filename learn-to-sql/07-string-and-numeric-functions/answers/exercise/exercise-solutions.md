# Exercise Solutions: Use String and Numeric Functions

## Exercise 1

```sql
SELECT
  title,
  length(title) AS title_length,
  upper(author) AS upper_author,
  substr(title, 1, 4) AS first_four
FROM books
ORDER BY title_length DESC, title;
```

Each expression creates a result column. The stored title and author stay unchanged.

## Exercise 2

```sql
SELECT upper(trim('   database   ')) AS prepared_word;
```

The inner `trim` returns `database`. The outer `upper` turns that result into `DATABASE`.

## Exercise 3

```sql
SELECT
  title,
  price,
  round(price * 1.075, 2) AS display_price
FROM books
ORDER BY book_id;
```

SQLite `REAL` is floating point, rounding rules are a business decision, and a display result does not define an exact storage model. Production money design must choose a suitable representation for the target database.
