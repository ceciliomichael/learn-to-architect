# Exercises: Understand NULL and Three-Valued Logic

## Exercise 1: Find known and unknown years

1. Find books with a missing publication year.
2. Find books with a known publication year.
3. Predict how many rows each query returns, then check.

## Exercise 2: Include missing values deliberately

1. Run `published_year <> 2024` and count the rows.
2. Write a condition that also includes missing years.
3. Explain why the counts differ.

## Exercise 3: Display without changing storage

1. Select title and publication year.
2. Display `Not recorded` for a missing year with `COALESCE`.
3. Query the missing row again and prove the stored value is still `NULL`.
