# Module 04: Sort, Limit, and Paginate Large Result Sets

## What You Will Learn

In this module, you will learn how to sort MySQL result rows with `ORDER BY`, eliminate duplicate rows using `DISTINCT`, and implement web application pagination formulas using `LIMIT count OFFSET offset` or `LIMIT offset, count`.

---

## Sorting Query Results (`ORDER BY`)

```sql
SELECT `title`, `unit_price` FROM `items` ORDER BY `unit_price` DESC;
```

### Multi-Column Sorting
```sql
SELECT `category`, `title`, `unit_price` 
FROM `items` 
ORDER BY `category` ASC, `unit_price` DESC;
```

---

## Removing Duplicates (`DISTINCT`)

```sql
SELECT DISTINCT `category` FROM `items`;
```

---

## Pagination in MySQL (`LIMIT`)

MySQL supports two equivalent `LIMIT` syntaxes:

1. Standard SQL: `LIMIT count OFFSET offset`
2. MySQL Alternative: `LIMIT offset, count`

```sql
-- Page 3 of API results (page size = 20 items, skipping first 40 items)
-- Formula: OFFSET = (page_number - 1) * page_size
SELECT `id`, `title`, `unit_price` 
FROM `items` 
ORDER BY `id` ASC 
LIMIT 20 OFFSET 40;
```

---

## Check Your Understanding

1. What is the offset calculation formula for page $P$ with page size $S$?
2. What is the equivalent MySQL syntax for `LIMIT 10 OFFSET 30`?
