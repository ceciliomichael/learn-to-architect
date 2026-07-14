# Exercises: PostgreSQL Types, Schemas, and Identity Columns

Use a disposable PostgreSQL database when available. Otherwise write and review the statements without claiming SQLite can execute them.

## Exercise 1: Design strong types

Create schema `learning` and a table for payments with identity ID, exact amount, three-letter currency, UTC instant, optional settlement date, and boolean refunded state. Add suitable checks.

## Exercise 2: Test enforcement

Insert valid rows, then try a negative amount, a four-letter currency, and invalid date input. Read the target errors and roll back the failed practice transaction.

## Exercise 3: Map from SQLite

Write a mapping for every `books` column to PostgreSQL. Explain price precision, missing year, stock boolean, and identity choice.
