# Module 08: Group and Aggregate Data

## What You Will Learn

In this module, you will learn how to summarize data using SQL aggregate functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`), group rows into summary buckets using `GROUP BY`, filter grouped results using `HAVING`, and understand the difference between `COUNT(*)` and `COUNT(column)`.

---

## Aggregate Functions

Aggregate functions compute a single summary result from a set of values:

- `COUNT(*)`: Counts all rows in a group (including NULL rows).
- `COUNT(column)`: Counts non-NULL entries in that column.
- `SUM(column)`: Sums numeric values (ignores NULL).
- `AVG(column)`: Computes average (ignores NULL).
- `MIN(column)` / `MAX(column)`: Returns minimum/maximum value.

```sql
SELECT COUNT(*) AS total_products, AVG(price) AS average_price FROM products;
```

---

## Grouping Summary Rows (`GROUP BY`)

`GROUP BY` collapses multiple rows sharing identical values in specified columns into summary rows:

```sql
SELECT category, COUNT(*) AS item_count, AVG(price) AS avg_price
FROM products
GROUP BY category;
```

---

## Filtering Group Summaries (`HAVING`)

- `WHERE` filters individual rows **before** grouping.
- `HAVING` filters aggregated group summary rows **after** `GROUP BY`.

```sql
SELECT category, COUNT(*) AS item_count
FROM products
GROUP BY category
HAVING COUNT(*) > 5;
```

---

## Step-by-Step Practical Example

```sql
CREATE TABLE sales (
  id INTEGER PRIMARY KEY,
  region TEXT NOT NULL,
  amount REAL NOT NULL
);

INSERT INTO sales VALUES
  (1, 'North', 100.0), (2, 'North', 150.0),
  (3, 'South', 200.0), (4, 'East', 50.0),
  (5, 'South', 300.0);

SELECT region, SUM(amount) AS total_sales
FROM sales
GROUP BY region
HAVING SUM(amount) >= 250.0;
```

### Output

```text
┌────────┬─────────────┐
│ region │ total_sales │
├────────┼─────────────┤
│ North  │ 250.0       │
│ South  │ 500.0       │
└────────┴─────────────┘
```

---

## Check Your Understanding

1. What is the difference between `WHERE` and `HAVING`?
2. How does `COUNT(*)` treat `NULL` values compared to `COUNT(column)`?
