# Exercise Solutions: Combine Result Sets

## Exercise 1

```sql
SELECT author AS person_name FROM books
UNION
SELECT customer_name FROM orders;

SELECT author AS person_name FROM books
UNION ALL
SELECT customer_name FROM orders;
```

`UNION ALL` retains repeated authors. `UNION` keeps each complete result row once.

## Exercise 2

```sql
CREATE TEMP TABLE list_a (name TEXT);
CREATE TEMP TABLE list_b (name TEXT);
INSERT INTO list_a VALUES ('Ava'), ('Noah'), ('Mira');
INSERT INTO list_b VALUES ('Mira'), ('Lena');

SELECT name FROM list_a INTERSECT SELECT name FROM list_b;
SELECT name FROM list_a EXCEPT SELECT name FROM list_b;
SELECT name FROM list_b EXCEPT SELECT name FROM list_a;
```

The intersection is Mira. The two differences point in opposite directions.

## Exercise 3

```sql
SELECT name AS item_name, price_cents / 100.0 AS price_amount,
       'active product' AS source
FROM products
WHERE active = 1
UNION ALL
SELECT name, price_cents / 100.0, 'inactive product'
FROM products
WHERE active = 0
ORDER BY price_amount DESC, item_name;
```

Every branch returns three corresponding columns.
