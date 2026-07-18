# Module 07: Use String and Numeric Functions

## What you will learn

You will transform result values with common SQLite functions and verify product-specific behavior before depending on it.

## A function returns a value

A function call has a name followed by arguments in parentheses:

```sql
SELECT title, length(title) AS title_length
FROM books;
```

SQLite's `length` returns the number of Unicode characters in text, not the storage bytes. A `NULL` input produces `NULL`.

## Change text case for display or comparison

```sql
SELECT
  upper(title) AS loud_title,
  lower(author) AS normalized_author
FROM books;
```

SQLite's built-in `upper` and `lower` only perform full case conversion for ASCII letters unless an extension supplies wider Unicode handling. Do not use simple case conversion as a complete international text matching strategy.

## Remove surrounding characters

```sql
SELECT trim('   SQL practice   ') AS cleaned;
```

`trim` removes spaces from both ends by default. `ltrim` removes from the left, and `rtrim` from the right. They do not change stored table data inside a `SELECT`.

## Take part of a text value

```sql
SELECT title, substr(title, 1, 5) AS first_five
FROM books;
```

SQLite text positions begin at 1. The example starts at the first character and takes five characters. A negative start counts from the end, which is SQLite behavior that should be checked before moving to another product.

## Work with numbers

```sql
SELECT
  title,
  price,
  round(price * 1.08, 2) AS price_with_tax
FROM books;
```

`round(value, digits)` returns a rounded result. It is useful for display, but money storage and exact decimal arithmetic require a deliberate database type and business rule. SQLite `REAL` uses floating-point values, so it is not a universal exact-money design.

Other useful functions are:

```sql
SELECT abs(-12) AS positive_value;
SELECT min(9, 4, 7) AS smallest_value;
SELECT max(9, 4, 7) AS largest_value;
```

In SQLite, multi-argument `min` and `max` act as scalar functions. Their behavior and names can differ in other database products. Aggregate forms are taught in Module 12.

## Nest functions carefully

The inner call runs first:

```sql
SELECT upper(trim('   ready   ')) AS cleaned_label;
```

This produces `READY`. Break complex expressions across lines and use an alias that describes the final meaning.

## Replace only truly missing input

Combine with Module 04:

```sql
SELECT
  title,
  length(COALESCE(author, '')) AS author_length
FROM books;
```

Use a fallback because it matches the requested meaning, not merely to eliminate `NULL`. Empty text is not the same fact as an unknown author.

## Portability habit

Before using a function in a project:

1. Check the target database's official documentation.
2. Confirm argument and `NULL` behavior.
3. Test non-ASCII text, boundaries, and numeric precision relevant to the project.
4. Keep product-specific functions in clearly identified code.

## Common mistakes

### Assuming every database has the same function

Even common tasks may use different names or arguments.

### Treating rounded display as exact storage

Rounding a query result does not change the underlying representation.

### Forgetting NULL propagation

Most scalar functions return `NULL` for a `NULL` input. Test and use a meaningful fallback only when appropriate.

## Check your understanding

You are ready when you can compose two functions, explain the result from inside outward, and identify which behavior must be checked for another database product.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
