# Module 04: Understand NULL and Three-Valued Logic

## What you will learn

You will test missing values correctly and understand why conditions can be true, false, or unknown.

## NULL is not an ordinary value

`NULL` represents missing or unknown information. In `books`, Web Basics has no known `published_year`.

It is not the number zero, an empty string, or the word `NULL`. Those are all different data.

## Test with IS NULL

```sql
SELECT title, published_year
FROM books
WHERE published_year IS NULL;
```

Use `IS NOT NULL` for known values:

```sql
SELECT title, published_year
FROM books
WHERE published_year IS NOT NULL;
```

Do not write `published_year = NULL`. Equality asks whether two known values are equal. When one side is unknown, the result is unknown rather than true.

## SQL conditions have three outcomes

A condition can be:

- True, so `WHERE` keeps the row
- False, so `WHERE` removes the row
- Unknown, so `WHERE` also removes the row

For the missing year, both of these comparisons are unknown:

```sql
published_year = 2024
published_year <> 2024
```

That is why this query does not include the missing year:

```sql
SELECT title, published_year
FROM books
WHERE published_year <> 2024;
```

To request known non-2024 years and missing years, say both parts:

```sql
SELECT title, published_year
FROM books
WHERE published_year <> 2024
   OR published_year IS NULL;
```

## AND and OR with unknown

Useful rules are:

- False `AND` unknown is false because both cannot be true.
- True `AND` unknown is unknown.
- True `OR` unknown is true because one side is already true.
- False `OR` unknown is unknown.

You do not need to memorize a large table. Ask whether the known side is enough to decide the whole condition.

## Show a fallback with COALESCE

`COALESCE` returns the first argument that is not `NULL`:

```sql
SELECT
  title,
  COALESCE(published_year, 'Year unknown') AS year_display
FROM books;
```

This changes only the displayed result. It does not replace the stored `NULL`.

Arguments should have compatible meanings. Mixing a number and text is convenient for display in SQLite, but strongly typed databases may choose or require a common result type. A more portable display can cast the number, a topic taught later.

## Missing is sometimes correct

Do not replace every `NULL` with zero. If zero would mean a real year, price, or count, it gives false information. Decide whether a value is required when designing the table, and use `NOT NULL` when the business rule truly requires it.

## Common mistakes

### Using `= NULL`

Use `IS NULL` or `IS NOT NULL`.

### Assuming not equal includes missing values

Unknown is not true. Add an explicit `IS NULL` branch if missing rows belong in the result.

### Using a display fallback as stored data

`COALESCE` in a query does not update the table.

## Check your understanding

You are ready when you can explain why ordinary comparison with `NULL` is unknown and write a condition that deliberately includes or excludes missing data.
