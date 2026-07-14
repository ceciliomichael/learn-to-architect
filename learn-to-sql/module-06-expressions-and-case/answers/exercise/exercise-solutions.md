# Exercise Solutions: Build Expressions and Decisions

## Exercise 1

```sql
SELECT
  title,
  price,
  price * 1.10 AS increased_price
FROM books
ORDER BY increased_price DESC, book_id;

SELECT title, price
FROM books
ORDER BY book_id;
```

The second result still shows original prices because the calculation was read-only.

## Exercise 2

```sql
SELECT title || ' by ' || author AS book_description
FROM books
ORDER BY book_id;
```

## Exercise 3

```sql
SELECT
  title,
  price,
  CASE
    WHEN price < 23 THEN 'Low'
    WHEN price < 32 THEN 'Middle'
    ELSE 'High'
  END AS price_label
FROM books
ORDER BY price, book_id;
```

Prices below 23 are Low. Prices from 23 up to but not including 32 are Middle. Prices 32 or higher are High.
