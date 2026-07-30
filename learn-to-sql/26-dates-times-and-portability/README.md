# Module 26: Work with Dates, Times, and Portability

## What you will learn

You will represent time consistently in SQLite, compare temporal types and date functions across MySQL and PostgreSQL, and write portable date logic.

---

## SQLite has no dedicated date storage class

SQLite commonly stores time values as:

- ISO 8601 text such as `2026-07-14 09:30:00`
- Unix timestamps as integer or real seconds from 1970-01-01 UTC
- Julian day numbers as real values

Choose one documented representation per column. Mixed representations make sorting and comparison unreliable. ISO text in a consistent most-significant-to-least-significant format sorts chronologically as text.

---

## Use SQLite date functions

```sql
SELECT date('2026-07-14') AS day;
SELECT datetime('2026-07-14 09:30:00', '+2 hours') AS later;
SELECT strftime('%Y-%m', '2026-07-14') AS year_month;
SELECT unixepoch('2026-07-14 00:00:00') AS epoch_seconds;
SELECT julianday('2026-07-15') - julianday('2026-07-14') AS day_difference;
```

SQLite date functions accept documented time-value formats and modifiers. Unsupported or invalid inputs often return `NULL`, so validate data at boundaries.

---

## Current time and UTC

```sql
SELECT datetime('now') AS current_utc;
```

SQLite's `now` uses UTC. A `localtime` modifier uses the operating environment and has platform and historical limits. Store event instants in UTC when appropriate and keep the original time-zone identifier when future local scheduling or legal display rules need it.

---

## Engine Temporal Comparison: SQLite vs. MySQL vs. PostgreSQL

When transitioning to production client-server engines like MySQL or PostgreSQL, you will work with dedicated native date and time data types instead of SQLite text strings:

| Engine | Types Available | Current UTC Timestamp Function | Date Arithmetic | Format Function |
| :--- | :--- | :--- | :--- | :--- |
| **SQLite** | Stored as `TEXT`, `INTEGER`, or `REAL` | `datetime('now')` | `datetime(col, '+1 day')` | `strftime('%Y-%m-%d', col)` |
| **MySQL** | `DATE`, `TIME`, `DATETIME`, `TIMESTAMP` | `NOW()` or `UTC_TIMESTAMP()` | `DATE_ADD(col, INTERVAL 1 DAY)` | `DATE_FORMAT(col, '%Y-%m-%d')` |
| **PostgreSQL** | `date`, `time`, `timestamp`, `timestamptz`, `interval` | `NOW()` or `CURRENT_TIMESTAMP` | `col + INTERVAL '1 day'` | `to_char(col, 'YYYY-MM-DD')` |

### Key Differences Between MySQL and PostgreSQL Temporal Types

1. **MySQL `DATETIME` vs `TIMESTAMP`**:
   - MySQL `DATETIME` stores a fixed calendar date and wall time (1000-01-01 to 9999-12-31) without timezone conversion.
   - MySQL `TIMESTAMP` converts inserted values from the session time zone to UTC for storage, and back to session time zone for retrieval (range: 1970 to 2038).
2. **PostgreSQL `timestamptz` (`timestamp with time zone`)**:
   - Converts input to a UTC instant internally, and renders it in the session time zone upon display.
3. **Date Arithmetic & String Format Dialects**:
   - SQLite uses `strftime()` and `datetime()`.
   - MySQL uses `DATE_FORMAT()`, `DATE_ADD()`, and `DATEDIFF()`.
   - PostgreSQL uses `to_char()`, standard SQL `INTERVAL '1 day'`, and `AGE()`.

---

## Date-only and instant are different meanings

- A birthday is normally a calendar date, not a UTC instant.
- A meeting in a named region may need local wall time and a zone identifier.
- A server event timestamp is often a UTC instant.

Choose storage from meaning before choosing a function.

---

## Common mistakes

### Storing locale-formatted text

`07/08/26` is ambiguous and does not sort safely. Use an agreed ISO form.

### Treating every date as midnight UTC

That changes the meaning of date-only facts across zones.

### Assuming an offset is a time zone

Regions can change offsets through seasonal and legal rules.

---

## Check your understanding

You are ready when you can choose between a date-only value and an instant, explain SQLite's three common representations, and contrast SQLite date functions with MySQL's `DATE_FORMAT()` and PostgreSQL's `timestamptz`.

---

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

