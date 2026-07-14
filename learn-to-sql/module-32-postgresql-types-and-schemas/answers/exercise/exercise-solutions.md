# Exercise Solutions: PostgreSQL Types, Schemas, and Identity Columns

## Exercise 1

```sql
CREATE SCHEMA learning;

CREATE TABLE learning.payments (
  payment_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  amount numeric(14, 2) NOT NULL CHECK (amount >= 0),
  currency text NOT NULL CHECK (char_length(currency) = 3),
  paid_at timestamp with time zone NOT NULL DEFAULT CURRENT_TIMESTAMP,
  settled_on date,
  refunded boolean NOT NULL DEFAULT false
);
```

Length alone does not prove a valid currency code. Production design can reference an approved currency table.

## Exercise 2

```sql
BEGIN;
INSERT INTO learning.payments (amount, currency)
VALUES (125.50, 'PHP');
INSERT INTO learning.payments (amount, currency)
VALUES (-1, 'PHP');
ROLLBACK;
```

Test each failure separately so one aborted PostgreSQL transaction does not hide later errors.

## Exercise 3

Use bigint identity for `book_id`, text for title and author, integer with a reasonable check for nullable published year, numeric with chosen scale for exact price rules, and boolean for stock. Preserve `NULL` for unknown publication year rather than inventing zero.
