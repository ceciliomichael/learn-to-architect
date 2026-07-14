# Exercise Solutions: Work with Dates, Times, and Portability

## Exercise 1

```sql
CREATE TABLE events (
  event_id INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  starts_at_utc TEXT NOT NULL
) STRICT;

INSERT INTO events (name, starts_at_utc) VALUES
  ('Open', '2026-07-14 01:00:00'),
  ('Review', '2026-07-14 03:30:00'),
  ('Close', '2026-07-15 00:00:00');

SELECT * FROM events ORDER BY starts_at_utc;
```

The consistent year-month-day and time order makes text sorting chronological.

## Exercise 2

```sql
SELECT name,
       date(starts_at_utc) AS event_date,
       strftime('%Y-%m', starts_at_utc) AS year_month,
       unixepoch(starts_at_utc) AS epoch_seconds,
       datetime(starts_at_utc, '+2 hours') AS two_hours_later
FROM events;
```

## Exercise 3

A birthday needs a date. A payment needs an instant, commonly stored in UTC. A recurring Manila meeting needs local wall-clock rules and the `Asia/Manila` zone identifier so future occurrences follow the intended region.
