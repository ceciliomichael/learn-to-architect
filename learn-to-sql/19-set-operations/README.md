# Module 19: Combine Result Sets

## What you will learn

You will stack compatible query results with union, intersection, and difference operations.

## UNION combines and removes duplicates

```sql
SELECT author AS person_name
FROM books
UNION
SELECT customer_name
FROM orders
ORDER BY person_name;
```

Each side must return the same number of columns, and corresponding values must be compatible. Result column names come from the first query. `UNION` removes duplicate result rows.

## UNION ALL keeps every row

```sql
SELECT author AS person_name
FROM books
UNION ALL
SELECT customer_name
FROM orders;
```

Use `UNION ALL` when duplicates are meaningful or inputs are already known to be disjoint. It avoids duplicate-removal work.

## INTERSECT keeps rows in both results

```sql
SELECT name FROM current_names
INTERSECT
SELECT name FROM approved_names;
```

`INTERSECT` uses distinct set behavior in SQLite. It finds result rows common to both sides.

## EXCEPT keeps rows only in the first result

```sql
SELECT name FROM current_names
EXCEPT
SELECT name FROM approved_names;
```

Direction matters. This returns current names that are not approved, not the reverse.

## ORDER BY belongs to the combined result

Place the ordinary final `ORDER BY` after the final query:

```sql
SELECT title AS label, price AS amount
FROM books
WHERE in_stock = 1
UNION ALL
SELECT name, price_cents / 100.0
FROM products
WHERE active = 1
ORDER BY amount DESC, label;
```

Sorting individual inputs requires nesting and is rarely meaningful unless it also determines which rows an input selects.

## Set operations combine vertically

Joins add related columns horizontally. Set operations stack compatible rows vertically. Choose from the requested result shape.

SQLite does not support every `ALL` variation that some products support for `INTERSECT` and `EXCEPT`. Check the target documentation.

## Common mistakes

### Different column counts

Every branch must return the same number.

### Using UNION when duplicates matter

Choose `UNION ALL` deliberately.

### Reversing EXCEPT

Say the request as first set minus second set.

## Check your understanding

You are ready when you can align result columns and predict duplicate behavior for each operation.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
