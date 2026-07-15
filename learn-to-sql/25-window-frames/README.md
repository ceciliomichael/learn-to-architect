# Module 25: Control Window Frames

## What you will learn

You will define exactly which ordered rows contribute to running and moving calculations.

## Partition and frame are different

A partition is the broad calculation group. A frame is the portion of that partition used for the current row by frame-sensitive window functions.

Write an explicit running total:

```sql
SELECT
  order_id,
  total_cents,
  SUM(total_cents) OVER (
    ORDER BY order_id
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
  ) AS running_total
FROM order_summaries
ORDER BY order_id;
```

For each current row, the frame begins at the partition start and ends at that physical row.

## Calculate a moving window

```sql
SELECT
  sale_day,
  amount,
  AVG(amount) OVER (
    ORDER BY sale_day
    ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
  ) AS three_row_average
FROM daily_sales;
```

The frame contains at most the current row and two preceding rows. This is three rows, not necessarily three calendar days if dates are missing or duplicated.

## Default frames can surprise you

When a frame-sensitive aggregate has window `ORDER BY` but no explicit frame, SQLite and PostgreSQL use a default similar to `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`. It includes peers equal on the ordering values.

With duplicate amounts, this can make a running total jump for all peer rows together. `ROWS` counts physical rows. `RANGE` groups by ordering values. `GROUPS` counts peer groups.

State the frame instead of relying on memory.

## Calculate across the full partition

Omit window ordering when it is unnecessary:

```sql
AVG(price) OVER (PARTITION BY author)
```

Or make a full ordered frame explicit:

```sql
AVG(price) OVER (
  PARTITION BY author
  ORDER BY published_year
  ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
)
```

The second form keeps ordering available while using the whole partition.

## first_value and last_value need frame attention

`last_value` returns the last value in the current frame, not automatically the last row of the entire partition. Use a full-partition frame when that is the request.

## Common mistakes

### Calling ROWS a time interval

It counts ordered rows. Use date logic for time periods.

### Assuming default running totals treat ties one by one

The default range frame includes peers.

### Forgetting the full frame for last_value

Define the intended end with `UNBOUNDED FOLLOWING`.

## Check your understanding

You are ready when you can describe the exact frame for one current row and predict how peers affect `ROWS` and `RANGE`.
