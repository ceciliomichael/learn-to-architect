# Module 14: Compute Across Rows with Window Functions

## What You Will Learn

In this module, you will learn how to use SQL Window Functions (`OVER()`, `PARTITION BY`, `ORDER BY`), perform analytical ranking (`ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`), calculate relative positional values (`LAG()`, `LEAD()`), and compute running totals across window frames.

---

## What is a Window Function?

Unlike `GROUP BY`, which collapses multiple rows into a single summary row, a **Window Function** computes dynamic metrics across a set of related rows while preserving individual row identities!

```sql
SELECT 
  name, 
  department, 
  salary,
  AVG(salary) OVER(PARTITION BY department) AS dept_avg_salary
FROM employees;
```

---

## Ranking Functions

- `ROW_NUMBER()`: Assigns a unique sequential integer (1, 2, 3...) to each row.
- `RANK()`: Assigns rank with gaps on ties (1, 2, 2, 4...).
- `DENSE_RANK()`: Assigns rank without gaps on ties (1, 2, 2, 3...).

```sql
SELECT 
  name, 
  salary,
  DENSE_RANK() OVER(ORDER BY salary DESC) AS salary_rank
FROM employees;
```

---

## Running Totals & Positional Navigation

```sql
-- Running Total across sales
SELECT 
  sale_date, 
  amount,
  SUM(amount) OVER(ORDER BY sale_date ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total,
  LAG(amount, 1) OVER(ORDER BY sale_date) AS prev_sale_amount
FROM sales;
```

---

## Check Your Understanding

1. How does `ROW_NUMBER()` differ from `RANK()` when duplicate values occur?
2. Why do window functions retain original table row output rather than collapsing rows?
