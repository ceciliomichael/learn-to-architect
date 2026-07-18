# Module 06: Build Expressions and Decisions

## What you will learn

You will calculate result values, combine text, and use `CASE` to choose a result based on conditions.

## Expressions create result values

```sql
SELECT
  title,
  price,
  price * 1.08 AS price_with_tax
FROM books;
```

The multiplication runs for each source row. It does not update the stored price.

Arithmetic operators include `+`, `-`, `*`, `/`, and `%`. Parentheses make calculation order clear:

```sql
SELECT title, (price + 5) * 2 AS example_total
FROM books;
```

SQLite division depends on value types. Dividing two integers performs integer division, while a real value produces a real result. Make the intended numeric kind visible:

```sql
SELECT 5 / 2 AS integer_result, 5.0 / 2 AS real_result;
```

SQLite returns 2 and 2.5. Numeric behavior differs among database products, so test the target product and use appropriate casts when precision matters.

## Join text with concatenation

SQLite and PostgreSQL use `||` for text concatenation:

```sql
SELECT title || ' by ' || author AS description
FROM books;
```

If an operand is `NULL`, the expression normally becomes `NULL`. Use `COALESCE` when a real fallback is appropriate.

## Choose a value with searched CASE

```sql
SELECT
  title,
  price,
  CASE
    WHEN price < 23 THEN 'budget'
    WHEN price < 32 THEN 'standard'
    ELSE 'premium'
  END AS price_band
FROM books;
```

SQL checks `WHEN` conditions from top to bottom and uses the result from the first true condition. If none is true, it uses `ELSE`. Without `ELSE`, the result is `NULL`.

Order matters. The second condition effectively covers prices from 23 through values below 32 because cheaper values already matched the first branch.

## CASE can turn stored codes into labels

```sql
SELECT
  title,
  CASE
    WHEN in_stock = 1 THEN 'Available'
    WHEN in_stock = 0 THEN 'Unavailable'
    ELSE 'Unknown state'
  END AS stock_status
FROM books;
```

This is display logic. It does not change the stored 1 or 0.

## Aliases and query clauses

A result alias is available to `ORDER BY` in the same query:

```sql
SELECT title, price * 1.08 AS price_with_tax
FROM books
ORDER BY price_with_tax DESC;
```

Do not rely on the same alias in `WHERE`. Logically, filtering happens before the result alias is created, and database products differ in nonstandard conveniences. Repeat a short expression or place the calculation in a subquery or CTE after those tools are taught.

## NULL in expressions

Most arithmetic involving `NULL` returns `NULL` because an unknown input makes the result unknown. `CASE` conditions follow three-valued logic and only choose a `WHEN` branch when its condition is true.

## Common mistakes

### Expecting a calculation to update the table

A selected expression only shapes the result.

### Writing broad CASE conditions first

Put more specific conditions before a broader condition that would also match them.

### Depending on integer division accidentally

Use a real operand when you need a fractional SQLite result and test portability requirements.

## Check your understanding

You are ready when you can calculate a result column, explain first-true `CASE` behavior, and distinguish displayed values from stored values.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
