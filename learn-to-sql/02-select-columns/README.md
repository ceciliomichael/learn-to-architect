# Module 02: Select Columns and Name Results

## What you will learn

You will choose exact result columns, control their order, and give them readable names.

## Reopen the course database

From `sql-course-practice`:

```text
sqlite3 library.db
```

Then set the display for this session:

```text
.headers on
.mode box
```

## Select only the facts you need

```sql
SELECT title, author
FROM books;
```

SQL reads the statement as a request for the `title` and `author` columns from the `books` table. The output column order follows the order in the `SELECT` list.

Change the list and the order changes:

```sql
SELECT author, title, price
FROM books;
```

The stored table has not changed. A query creates a result table for you to read.

## Prefer explicit columns in real work

`SELECT *` is useful for first inspection and small practice tables. Explicit columns are usually clearer because they:

- Show which data the query needs
- Keep a stable result shape when a table gains another column
- Avoid reading large or private columns by accident
- Let you choose a useful order

Use `*` deliberately, not automatically.

## Give a result column an alias

```sql
SELECT
  title AS book_title,
  author AS written_by
FROM books;
```

An alias changes the heading in this query result. It does not rename the stored column.

For a heading with spaces, quote the identifier:

```sql
SELECT title AS "Book Title"
FROM books;
```

Simple names such as `book_title` are easier to use in later queries and programs.

## Format longer statements

SQL allows spaces and line breaks between its pieces. This is the same request:

```sql
SELECT book_id, title, price
FROM books;
```

Use one selected item per line when the list grows:

```sql
SELECT
  book_id,
  title,
  published_year,
  price
FROM books;
```

Readable formatting helps you check commas and understand each clause.

## Duplicate values are still separate rows

```sql
SELECT author
FROM books;
```

Mira Chen and Lena Ortiz each appear twice because the query returns one selected value for every source row. Module 05 teaches how to request unique values.

## SQL results have no promised order yet

The rows may appear in identifier order during this small example, but SQL does not promise that order without `ORDER BY`. Do not describe an unstated order as part of a query's meaning. Sorting is taught in Module 05.

## Common mistakes

### Leaving out a comma

Each selected column must be separated by a comma. The final item before `FROM` has no comma.

### Thinking an alias edits the table

Run `.schema books` and you will see the stored column name is unchanged.

### Assuming the visible row order is guaranteed

Storage and query plans can change. Only `ORDER BY` defines result order.

## Check your understanding

You are ready when you can request three columns in a chosen order and explain why an alias changes only the result heading.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
