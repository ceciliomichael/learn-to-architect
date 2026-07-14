# Module 05: Sort, Remove Duplicates, and Limit Results

## What you will learn

You will define result order, request unique values, and take a predictable part of a result.

## ORDER BY defines row order

```sql
SELECT title, price
FROM books
ORDER BY price ASC;
```

`ASC` means ascending and is the default. `DESC` means descending:

```sql
SELECT title, price
FROM books
ORDER BY price DESC;
```

Without `ORDER BY`, SQL does not promise an order.

## Resolve ties with another key

Two rows can have the same first sort value. Add another expression for a stable order:

```sql
SELECT title, author
FROM books
ORDER BY author ASC, title ASC;
```

SQL sorts by author first. Within one author, it sorts by title. For pagination or repeatable output, finish with a unique key when other selected sort values may tie:

```sql
ORDER BY price DESC, book_id ASC
```

## Sort by a selected alias

```sql
SELECT title, price AS listed_price
FROM books
ORDER BY listed_price DESC;
```

SQL permits result aliases in `ORDER BY`. This is often clearer when the selected expression is long.

## NULL placement differs among products

SQLite treats `NULL` as smaller than other values for ordinary ordering, so it appears first with `ASC` and last with `DESC`. Other database products offer different defaults or `NULLS FIRST` and `NULLS LAST` controls.

To state a cross-product intention explicitly, sort by the test first:

```sql
SELECT title, published_year
FROM books
ORDER BY published_year IS NULL, published_year;
```

False sorts before true, so known years appear before missing years in SQLite.

## Request distinct result rows

```sql
SELECT DISTINCT author
FROM books
ORDER BY author;
```

`DISTINCT` removes duplicate result rows. With several selected columns, the entire combination must be equal:

```sql
SELECT DISTINCT author, in_stock
FROM books;
```

This does not mean one row per author because an author can have books with different stock values.

## Limit after ordering

```sql
SELECT title, price
FROM books
ORDER BY price DESC, book_id
LIMIT 3;
```

This means the three highest-priced rows. Without `ORDER BY`, it only means some three rows and is not a reliable top-three request.

Skip rows with `OFFSET`:

```sql
SELECT title, price
FROM books
ORDER BY price DESC, book_id
LIMIT 2 OFFSET 2;
```

Large offsets can become slow and results can shift if rows change between requests. Production pagination often remembers the last sort key instead. The key lesson is that pagination needs a complete deterministic order.

## Logical reading order

For the clauses learned so far, reason in this order:

1. `FROM` chooses source rows.
2. `WHERE` keeps matching rows.
3. `SELECT` creates result columns.
4. `DISTINCT` removes duplicate result rows.
5. `ORDER BY` sorts them.
6. `LIMIT` and `OFFSET` choose a portion.

This is a reasoning model, not a claim about every internal optimization.

## Common mistakes

### Calling the first visible rows the top rows

Top has no meaning until an order is defined.

### Using DISTINCT to hide a bad join

Unexpected duplicates often reveal a relationship mistake. Understand their cause before removing them.

### Sorting by a nonunique value for pages

Add a unique final key so tied rows have a stable relative order.

## Check your understanding

You are ready when you can write a deterministic top-N query and explain what counts as a duplicate for a multi-column `DISTINCT`.
