# Module 30: Use Triggers Carefully

## What you will learn

You will run database logic after a row event, create an audit record, and recognize when triggers create harmful hidden behavior.

## A trigger reacts to an event

Create an audit table:

```sql
CREATE TABLE product_price_audit (
  audit_id INTEGER PRIMARY KEY,
  product_id INTEGER NOT NULL,
  old_price_cents INTEGER NOT NULL,
  new_price_cents INTEGER NOT NULL,
  changed_at_utc TEXT NOT NULL
) STRICT;
```

Create an SQLite row trigger:

```sql
CREATE TRIGGER products_price_audit
AFTER UPDATE OF price_cents ON products
FOR EACH ROW
WHEN OLD.price_cents <> NEW.price_cents
BEGIN
  INSERT INTO product_price_audit
    (product_id, old_price_cents, new_price_cents, changed_at_utc)
  VALUES
    (NEW.product_id, OLD.price_cents, NEW.price_cents, datetime('now'));
END;
```

`OLD` contains the row before the update. `NEW` contains it after. The `WHEN` avoids an audit row when the value did not actually change.

## Timing and event decide available rows

- Insert triggers have `NEW` but no `OLD` row.
- Delete triggers have `OLD` but no `NEW` row.
- Update triggers have both.

SQLite supports `BEFORE`, `AFTER`, and `INSTEAD OF` triggers. Prefer `AFTER` for simple auditing. SQLite documents cautions around modifying or deleting rows from a `BEFORE` trigger and around undefined new row identifiers.

## Triggers run inside the statement transaction

If the audit insert fails, the outer update normally fails too under ordinary conflict behavior. Rolling back the transaction rolls back trigger changes.

## Hidden behavior has costs

Triggers can keep rules near data, but readers may not know they run. Risks include:

- Unexpected extra writes and locks
- Recursive trigger chains
- Difficult migration ordering
- Logic duplicated with application code
- Product-specific behavior

Use a trigger when the rule must hold for every database writer and is clearer there. Use explicit application or service logic when orchestration, external calls, or complex user feedback is needed. Never call external services from a database trigger.

## Inspect and remove

```text
.schema products_price_audit
```

```sql
DROP TRIGGER products_price_audit;
```

Document each trigger's event, affected tables, failure behavior, and tests.

## Common mistakes

### Auditing an unchanged value

Use a `WHEN` comparison appropriate for possible `NULL` values. The example columns are nonmissing.

### Creating a trigger loop

Map every table the trigger writes and configure recursive behavior deliberately.

### Assuming RETURNING includes trigger rows

SQLite's top-level `RETURNING` does not report additional trigger changes.

## Check your understanding

You are ready when you can identify `OLD` and `NEW`, predict transaction behavior, and justify why a trigger is clearer than explicit code.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
