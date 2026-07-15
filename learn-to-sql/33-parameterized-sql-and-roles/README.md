# Module 33: Parameterized SQL, Roles, and Least Privilege

## What you will learn

You will separate data from SQL text, restrict dynamic identifiers, and grant only the database abilities an application needs.

## SQL injection begins when data becomes code

Unsafe application logic joins user text into an SQL string:

```text
query = "SELECT * FROM users WHERE email = '" + user_input + "'"
```

Quotes and SQL syntax inside the input can change the statement's structure. Escaping by hand is fragile and product-specific.

## Bind values as parameters

Write fixed SQL and pass values separately through the database library:

```sql
SELECT user_id, email
FROM users
WHERE email = ?;
```

SQLite APIs commonly use `?` or named parameters. PostgreSQL client libraries often use `$1` at the server protocol level or a driver-specific placeholder:

```sql
SELECT user_id, email
FROM app.users
WHERE email = $1;
```

The application sends SQL structure and parameter values separately. The driver handles representation. Parameters also improve type handling and can support statement reuse.

## Parameters are for values, not identifiers

You cannot normally bind a table name, column name, sort direction, or SQL keyword as a value parameter. For a user-selectable sort, map an allowed choice to fixed code:

```text
"price" -> "ORDER BY price_cents"
"name"  -> "ORDER BY name"
```

Reject every choice outside the allowlist. Never paste a raw identifier from user input.

## Least privilege limits damage

In PostgreSQL, roles can own objects, receive privileges, and inherit other roles. An application runtime role usually should not own schema objects or have permission to drop tables.

A simplified reviewed setup might include:

```sql
CREATE ROLE shop_runtime LOGIN;

GRANT USAGE ON SCHEMA app TO shop_runtime;
GRANT SELECT, INSERT, UPDATE ON app.orders TO shop_runtime;
GRANT SELECT, INSERT, UPDATE ON app.order_items TO shop_runtime;
GRANT SELECT ON app.products TO shop_runtime;
```

Identity sequences and functions can need their own privileges depending on definitions and PostgreSQL behavior. Test every required operation and confirm forbidden operations fail.

Migration roles, read-only reporting roles, and runtime roles should be separate.

## Ownership and default privileges matter

The object owner has powerful control. `GRANT` adds permissions and `REVOKE` removes them, subject to ownership and inherited privileges.

```sql
REVOKE CREATE ON SCHEMA public FROM PUBLIC;
```

Whether this is needed depends on PostgreSQL version, database creation defaults, and existing policy. Audit current privileges rather than copying one hardening command blindly.

Use `ALTER DEFAULT PRIVILEGES` carefully for the object-creating role so future objects receive intended grants. It does not retroactively change existing objects.

## Protect credentials and sensitive data

- Keep credentials outside source code and logs.
- Use a secret manager or protected deployment configuration.
- Rotate leaked secrets.
- Require encrypted network connections and verify server identity where applicable.
- Avoid broad production data access for developers and analytics.
- Do not log raw parameter values that contain credentials or personal data.

## Common mistakes

### Parameterizing only some inputs

Every untrusted value uses binding. Dynamic identifiers use strict allowlists.

### Giving the application owner privileges

Use a separate migration owner and narrow runtime role.

### Assuming ORM use prevents injection

Raw fragments, dynamic order clauses, and unsafe APIs can still construct code.

## Check your understanding

You are ready when you can explain code-data separation and design a role that can do required work but cannot change the schema.
