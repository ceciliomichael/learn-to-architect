# Module 32: Client-Server Types, Schemas, and Identity Columns (PostgreSQL & MySQL)

## What you will learn

You will move from SQLite's flexible type model to strict type enforcement, namespace schemas, and auto-increment identity columns in production client-server databases like PostgreSQL and MySQL.

---

## Production Type Mapping Matrix (SQLite vs. MySQL vs. PostgreSQL)

When migrating or building schemas for MySQL or PostgreSQL, map your SQLite dynamic types to exact production types:

| Data Meaning | SQLite Type | MySQL / MariaDB Type | PostgreSQL Type |
| :--- | :--- | :--- | :--- |
| **Auto-Increment Primary Key** | `INTEGER PRIMARY KEY AUTOINCREMENT` | `BIGINT AUTO_INCREMENT PRIMARY KEY` | `bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY` |
| **Variable Length Text** | `TEXT` | `VARCHAR(255)` or `TEXT` | `varchar(255)` or `text` |
| **Exact Currency / Decimal** | `REAL` or `NUMERIC` | `DECIMAL(12, 2)` | `numeric(12, 2)` |
| **Boolean State** | `INTEGER` (`1` / `0`) | `TINYINT(1)` or `BOOLEAN` | `boolean` (`true` / `false`) |
| **Date & Time (Instant)** | `TEXT` (ISO 8601 string) | `DATETIME` or `TIMESTAMP` | `timestamp with time zone` (`timestamptz`) |
| **JSON Data** | `TEXT` (with JSON functions) | `JSON` | `jsonb` |

---

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

---

## MySQL equivalent table creation

In MySQL, the equivalent strict table definition is written as:

```sql
CREATE TABLE catalog_products (
  product_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  active BOOLEAN NOT NULL DEFAULT TRUE,
  price DECIMAL(12, 2) NOT NULL CHECK (price >= 0),
  available_on DATE,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

Notice the syntax differences:
- MySQL uses `BIGINT AUTO_INCREMENT` instead of `GENERATED ALWAYS AS IDENTITY`.
- MySQL uses `DECIMAL` instead of `numeric` (both represent exact decimals).
- MySQL uses `VARCHAR(255)` for bounded text strings.

---

## Choose numeric meaning

- `smallint`, `integer`, and `bigint` store whole numbers with defined ranges.
- `numeric(precision, scale)` / `DECIMAL(precision, scale)` stores exact decimal values under declared limits.
- `real` and `double precision` are approximate floating-point types.

Exact decimal does not decide currency conversion, rounding timing, or legal rules. Those remain domain decisions.

---

## Use real boolean and temporal types

PostgreSQL `boolean` uses true, false, or `NULL`. `date` stores a calendar date. `timestamp without time zone` stores a date and time without an instant zone interpretation. `timestamp with time zone` stores an instant, converts input to UTC internally, and displays it in the session time zone.

---

## Use identity for generated keys

```sql
product_id bigint GENERATED ALWAYS AS IDENTITY
```

Identity columns are the modern standard SQL form for sequence-backed generated values. `ALWAYS` rejects an explicit value unless the statement uses an override. `BY DEFAULT` allows explicit values. Neither guarantees gap-free numbering because rollbacks and sequence allocation can leave gaps.

---

## Use specialized types deliberately

PostgreSQL includes `uuid`, arrays, ranges, network address types, enums, and `jsonb`.

`jsonb` is useful for document-shaped attributes that vary or need containment queries. It should not replace ordinary columns and foreign keys for stable relational facts. Validate required JSON shape in the application and with suitable database constraints where practical.

---

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

---

## Convert from SQLite deliberately

1. Map every SQLite representation to business meaning.
2. Clean values that strong target types reject.
3. Define keys and constraints explicitly.
4. Convert dates and times with known source zones.
5. Test row counts, aggregates, relationships, and edge values.

Do not copy a SQLite file schema mechanically and assume equivalent behavior.

---

## Common mistakes

### Using serial without understanding identity

Identity is the clearer modern declaration for new schemas in PostgreSQL, while MySQL uses `AUTO_INCREMENT`.

### Calling timestamp with time zone a stored zone name

It stores an instant, not the original region name.

### Putting every changing field in JSONB / JSON

Stable searchable relationships still deserve typed relational columns.

---

## Check your understanding

You are ready when you can choose exact or approximate numeric types, explain identity gaps, compare SQLite auto-increment with MySQL `AUTO_INCREMENT` and PostgreSQL `IDENTITY`, and qualify a table by schema.

---

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
