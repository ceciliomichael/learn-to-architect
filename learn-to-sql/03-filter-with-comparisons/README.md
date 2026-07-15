# Module 03: Filter Rows with Comparisons

## What you will learn

You will use `WHERE` to keep rows that meet clear conditions and combine conditions without changing their meaning.

## WHERE tests each source row

```sql
SELECT title, price
FROM books
WHERE price < 25;
```

For each book row, SQLite checks whether its price is less than 25. Only rows where the condition is true enter the result.

Common comparison operators are:

```text
=   equal
<>  not equal
<   less than
<=  less than or equal
>   greater than
>=  greater than or equal
```

Use one `=` for SQL equality:

```sql
SELECT title
FROM books
WHERE author = 'Mira Chen';
```

Text values use single quotes. Identifiers such as `author` do not.

## Combine conditions

`AND` requires both conditions:

```sql
SELECT title, price
FROM books
WHERE price < 30
  AND in_stock = 1;
```

`OR` requires at least one:

```sql
SELECT title, author
FROM books
WHERE author = 'Mira Chen'
   OR author = 'Lena Ortiz';
```

`NOT` reverses a condition:

```sql
SELECT title
FROM books
WHERE NOT in_stock = 1;
```

For this table, that finds rows with `in_stock` equal to 0. Module 04 explains why missing values require additional care.

## Parentheses preserve your intention

`AND` is evaluated before `OR`. Do not make a reader memorize precedence when parentheses can show the rule:

```sql
SELECT title, author, price
FROM books
WHERE (author = 'Mira Chen' OR author = 'Lena Ortiz')
  AND price < 30;
```

This finds lower-priced books by either named author. Without the parentheses, every Mira Chen row could pass regardless of price.

## Test a range with BETWEEN

```sql
SELECT title, price
FROM books
WHERE price BETWEEN 22 AND 31;
```

`BETWEEN` includes both endpoints. The example includes prices equal to 22 and 31.

## Match a list with IN

```sql
SELECT title, published_year
FROM books
WHERE published_year IN (2020, 2021, 2024);
```

This is clearer than repeating three equality comparisons joined by `OR`.

## Match text patterns with LIKE

`%` matches zero or more characters. `_` matches exactly one character.

```sql
SELECT title
FROM books
WHERE title LIKE '%Data%';
```

This finds titles containing `Data`.

```sql
SELECT title
FROM books
WHERE title LIKE 'Web _asics';
```

In SQLite's default behavior, `LIKE` is case-insensitive for ordinary ASCII letters. Unicode and other database products can behave differently. Do not use that SQLite behavior as a universal promise.

## Filtering does not change stored rows

A `SELECT` with `WHERE` reads. It does not delete rows that fail the condition. Data-changing statements are taught only after safe preview habits are established.

## Common mistakes

### Writing `==` from another language

Use standard SQL `=`. SQLite accepts `==`, but it is not the portable form taught here.

### Forgetting text quotes

`Mira Chen` without single quotes is treated as identifiers and causes an error.

### Mixing AND and OR without parentheses

Write the intended groups explicitly, then test each smaller condition separately.

## Check your understanding

You are ready when you can translate a plain-language request into comparisons and parentheses, then predict which rows pass.
