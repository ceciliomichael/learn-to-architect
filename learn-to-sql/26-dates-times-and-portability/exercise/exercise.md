# Exercises: Work with Dates, Times, and Portability

## Exercise 1: Store consistent events

Create strict `events(event_id INTEGER PRIMARY KEY, name TEXT NOT NULL, starts_at_utc TEXT NOT NULL)` and insert three ISO timestamps. Sort them and explain why the format works.

## Exercise 2: Calculate and format

For each event, display the date, year-month, Unix timestamp, and a value two hours later using SQLite functions.

## Exercise 3: Classify meanings

For birthday, online payment time, and weekly meeting in Asia/Manila, write which information must be stored and why one representation does not fit all three.
