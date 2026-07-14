# Exercises: Tune Queries with Evidence

## Exercise 1: Define a workload

Write a performance requirement for one shop query. Include data size, result limit, concurrency, latency percentile, and read or write frequency.

## Exercise 2: Compare one focused change

Generate many disposable product rows, record the SQLite plan and timing for category-active-price search, add one matching composite or partial index, then repeat. Record read improvement and insert cost considerations.

## Exercise 3: Read a PostgreSQL plan responsibly

In a disposable PostgreSQL database, run plain `EXPLAIN`, then safe `EXPLAIN (ANALYZE, BUFFERS)` for a select. Compare estimated and actual rows. Write one hypothesis, make one change, and measure again.
