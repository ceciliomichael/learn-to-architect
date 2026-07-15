# Exercise Solutions: Select Columns and Name Results

## Exercise 1

```sql
SELECT title, price
FROM books;
```

The headings are `title` and `price`. Reverse them with:

```sql
SELECT price, title
FROM books;
```

Only the result column order changes.

## Exercise 2

```sql
SELECT
  book_id AS id,
  title AS book_title,
  published_year AS year_published
FROM books;
```

Then run:

```text
.schema books
```

The schema still contains `book_id`, `title`, and `published_year` because aliases belong only to the result.

## Exercise 3

```sql
SELECT author
FROM books;
```

There are six result rows because there are six source book rows. Repeated values remain because no duplicate-removal operation was requested. The visible order is not guaranteed without `ORDER BY`.
