# Module 26: Work with Dates, Times, and Portability

## What you will learn

You will represent time consistently in SQLite and recognize where PostgreSQL uses dedicated temporal types.

## SQLite has no dedicated date storage class

SQLite commonly stores time values as:

- ISO 8601 text such as `2026-07-14 09:30:00`
- Unix timestamps as integer or real seconds from 1970-01-01 UTC
- Julian day numbers as real values

Choose one documented representation per column. Mixed representations make sorting and comparison unreliable.

ISO text in a consistent most-significant-to-least-significant format sorts chronologically as text.

## Use SQLite date functions

```sql
SELECT date('2026-07-14') AS day;
SELECT datetime('2026-07-14 09:30:00', '+2 hours') AS later;
SELECT strftime('%Y-%m', '2026-07-14') AS year_month;
SELECT unixepoch('2026-07-14 00:00:00') AS epoch_seconds;
SELECT julianday('2026-07-15') - julianday('2026-07-14') AS day_difference;
```

SQLite date functions accept documented time-value formats and modifiers. Unsupported or invalid inputs often return `NULL`, so validate data at boundaries.

## Current time and UTC

```sql
SELECT datetime('now') AS current_utc;
```

SQLite's `now` uses UTC. A `localtime` modifier uses the operating environment and has platform and historical limits. Store event instants in UTC when appropriate and keep the original time-zone identifier when future local scheduling or legal display rules need it.

An offset alone, such as `+08:00`, does not preserve a region's daylight-saving rules.

## Date-only and instant are different meanings

- A birthday is normally a calendar date, not a UTC instant.
- A meeting in a named region may need local wall time and a zone identifier.
- A server event timestamp is often a UTC instant.

Choose storage from meaning before choosing a function.

## PostgreSQL uses temporal types

PostgreSQL has `date`, `time`, `timestamp without time zone`, `timestamp with time zone`, and `interval`. Its `timestamp with time zone` represents an instant and displays it using the session time zone; it does not preserve the originally written zone name.

SQL products differ in parsing, precision, interval arithmetic, and time-zone data. Keep product-specific operations labeled and tested.

## Common mistakes

### Storing locale-formatted text

`07/08/26` is ambiguous and does not sort safely. Use an agreed ISO form.

### Treating every date as midnight UTC

That changes the meaning of date-only facts across zones.

### Assuming an offset is a time zone

Regions can change offsets through seasonal and legal rules.

## Check your understanding

You are ready when you can choose between a date-only value and an instant and explain SQLite's three common representations.
