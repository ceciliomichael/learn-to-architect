# Module 03: Filter Rows, Operators, and Handling `NULL`

## What You Will Learn

In this module, you will learn how to filter data in MySQL using `WHERE`, comparison operators, pattern matching (`LIKE`), list comparisons (`IN`), range filtering (`BETWEEN`), handling `NULL` values using `IS NULL`, and MySQL's null-handling functions `IFNULL()` and `COALESCE()`.

---

## The `WHERE` Clause in MySQL

```sql
SELECT * FROM `items` WHERE `unit_price` >= 100.00;
```

### Key Comparison & Logical Operators

- `=`, `!=`, `<>`, `<`, `>`, `<=`, `>=`
- `BETWEEN min AND max`
- `IN ('val1', 'val2')`
- `LIKE '%search%'` (`%` multi-character wildcard, `_` single-character wildcard)
- `AND`, `OR`, `NOT`

---

## Handling `NULL` in MySQL

`NULL` represents missing data. Equality comparisons (`= NULL`) evaluate to `UNKNOWN`.

- `IS NULL` / `IS NOT NULL`
- `IFNULL(expr1, expr2)`: MySQL-specific function returning `expr2` if `expr1` is NULL.
- `COALESCE(expr1, expr2, ...)`: Standard SQL function returning the first non-NULL argument.

```sql
SELECT `title`, IFNULL(`discount_price`, `unit_price`) AS `effective_price`
FROM `items`
WHERE `discount_price` IS NOT NULL;
```

---

## Check Your Understanding

1. What does `IFNULL(a, b)` return if `a` is not NULL?
2. Why must you use `IS NULL` instead of `= NULL` in MySQL `WHERE` clauses?
