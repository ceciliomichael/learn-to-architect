# Module 14: Join Matching Rows

## What you will learn

You will connect rows through keys, qualify column names, and avoid accidental row multiplication.

## Relationships replace repeated text

In `shop.db`, a product stores `category_id`, not a repeated category name. The foreign key keeps that identifier valid. A join reads related facts together.

```sql
SELECT
  p.product_id,
  p.name AS product_name,
  c.name AS category_name
FROM products AS p
INNER JOIN categories AS c
  ON c.category_id = p.category_id
ORDER BY p.product_id;
```

`p` and `c` are table aliases. `p.name` clearly means the product name, while `c.name` means the category name.

For each product, the join finds category rows where the key values match. `INNER JOIN` keeps only matching combinations.

## Think about result grain

The query returns one row per matching product because:

- Each product has one category identifier.
- A category primary key matches at most one category row.

State the expected grain before writing a join. If both sides can match many rows, the result can multiply.

## Join and then filter

```sql
SELECT p.name, c.name AS category_name, p.price_cents
FROM products AS p
INNER JOIN categories AS c
  ON c.category_id = p.category_id
WHERE p.active = 1
  AND c.name = 'Books'
ORDER BY p.name;
```

`ON` explains the relationship. `WHERE` applies result requirements. For inner joins, some predicates can produce the same rows in either place, but separating relationship from filter improves meaning and prepares you for outer joins.

## Join several tables one relationship at a time

The pattern is:

```sql
FROM first_table AS a
JOIN second_table AS b ON b.key = a.second_key
JOIN third_table AS c ON c.key = b.third_key
```

After each join, ask how many rows one input row can match.

## A missing or wrong ON condition is dangerous

This produces every product combined with every category:

```sql
SELECT p.name, c.name
FROM products AS p
CROSS JOIN categories AS c;
```

A Cartesian product is useful when every combination is intended. It is usually a bug when a relationship condition was forgotten. Count and inspect small samples before trusting a large join.

Do not add `DISTINCT` merely to hide unexpected duplicates. Fix the relationship or result grain.

## Common mistakes

### Joining unrelated columns with similar names

Follow declared keys and domain meaning, not spelling alone.

### Leaving duplicate column names unqualified

Use table aliases and qualify them.

### Assuming one match without a constraint

Uniqueness must be enforced or proven. Otherwise one row can match several.

## Check your understanding

You are ready when you can predict the result grain and explain every `ON` equality through a key relationship.
