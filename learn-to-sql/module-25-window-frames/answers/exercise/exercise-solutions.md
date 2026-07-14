# Exercise Solutions: Control Window Frames

## Setup and Exercise 1

```sql
CREATE TEMP TABLE daily_sales (sale_day TEXT, amount INTEGER);
INSERT INTO daily_sales VALUES
  ('2026-01-01', 10), ('2026-01-02', 20),
  ('2026-01-02', 5), ('2026-01-03', 15), ('2026-01-04', 25);

SELECT sale_day, amount,
       SUM(amount) OVER (
         ORDER BY sale_day
         ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS row_running_total
FROM daily_sales;
```

## Exercise 2

```sql
SELECT sale_day, amount,
       SUM(amount) OVER (
         ORDER BY sale_day
         ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS rows_total,
       SUM(amount) OVER (ORDER BY sale_day) AS default_total
FROM daily_sales;
```

The default includes both rows sharing the same date as peers, while `ROWS` advances physical row by physical row. Add a unique tie breaker when physical order must be deterministic.

## Exercise 3

```sql
SELECT sale_day, amount,
       AVG(amount) OVER (
         ORDER BY sale_day, rowid
         ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS moving_average,
       AVG(amount) OVER (
         ORDER BY sale_day, rowid
         ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
       ) AS full_average
FROM daily_sales;
```
