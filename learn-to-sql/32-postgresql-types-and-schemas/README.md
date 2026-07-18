# Module 32: PostgreSQL Types, Schemas, and Identity Columns

## What you will learn

You will move from SQLite's type model to PostgreSQL's stronger types, namespace schemas, and standard identity columns.

## PostgreSQL columns have enforced types

```sql
CREATE TABLE catalog.products (
  product_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  name text NOT NULL,
  active boolean NOT NULL DEFAULT true,
  price numeric(12, 2) NOT NULL CHECK (price >= 0),
  available_on date,
  created_at timestamp with time zone NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

PostgreSQL converts compatible input or rejects it. It does not use SQLite's per-value storage classes and affinities.

## Choose numeric meaning

- `smallint`, `integer`, and `bigint` store whole numbers with defined ranges.
- `numeric(precision, scale)` stores exact decimal values under declared limits.
- `real` and `double precision` are approximate floating-point types.

Exact decimal does not decide currency conversion, rounding timing, or legal rules. Those remain domain decisions.

## Use real boolean and temporal types

PostgreSQL `boolean` uses true, false, or `NULL`. `date` stores a calendar date. `timestamp without time zone` stores a date and time without an instant zone interpretation. `timestamp with time zone` stores an instant, converts input to UTC internally, and displays it in the session time zone.

## Use identity for generated keys

```sql
product_id bigint GENERATED ALWAYS AS IDENTITY
```

Identity columns are the modern SQL form for sequence-backed generated values. `ALWAYS` rejects an explicit value unless the statement uses an override. `BY DEFAULT` allows explicit values. Neither guarantees gap-free numbering because rollbacks and sequence allocation can leave gaps.

## Use specialized types deliberately

PostgreSQL includes `uuid`, arrays, ranges, network address types, enums, and `jsonb`.

`jsonb` is useful for document-shaped attributes that vary or need containment queries. It should not replace ordinary columns and foreign keys for stable relational facts. Validate required JSON shape in the application and with suitable database constraints where practical.

## Schemas are namespaces

```sql
CREATE SCHEMA catalog;
CREATE TABLE catalog.categories (
  category_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  name text NOT NULL UNIQUE
);
```

The qualified name has schema and object. Different schemas can contain tables with the same unqualified name.

`search_path` controls how PostgreSQL resolves an unqualified name. Creating objects or calling functions from schemas writable by untrusted roles can be a security risk. Production code should use controlled paths and qualified names where ambiguity matters.

## Convert from SQLite deliberately

1. Map every SQLite representation to business meaning.
2. Clean values that strong target types reject.
3. Define keys and constraints explicitly.
4. Convert dates and times with known source zones.
5. Test row counts, aggregates, relationships, and edge values.

Do not copy a SQLite file schema mechanically and assume equivalent behavior.

## Common mistakes

### Using serial without understanding identity

Identity is the clearer modern declaration for new schemas.

### Calling timestamp with time zone a stored zone name

It stores an instant, not the original region name.

### Putting every changing field in JSONB

Stable searchable relationships still deserve typed relational columns.

## Check your understanding

You are ready when you can choose exact or approximate numeric types, explain identity gaps, and qualify a table by schema.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
