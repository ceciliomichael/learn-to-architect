# Exercise Solutions: Module 39

## 1. Trace the graph

The CLI package can know about the command-line parser because it owns the process interface.

The domain package is the best home for reusable business rules because both storage and CLI can depend on it without forcing the domain to know about those mechanisms.

Under the shown graph, domain does not depend on storage and therefore cannot call storage directly.

This is intentional dependency direction, not a limitation to work around.

## 2. Repair a feature design

The sqlite/postgres feature pair is fragile if code assumes exactly one is enabled because Cargo feature unification can produce a build where both are enabled.

One cleaner design is:

~~~text
application configuration
          |
          v
choose Storage implementation
       /       \
      v         v
 SQLite      Postgres
~~~

That choice can occur at runtime.

Another valid design is separate adapter packages:

~~~text
storage-api
  ^      ^
  |      |
sqlite  postgres
~~~

The correct design depends on distribution and compilation requirements, but ordinary additive features should not secretly mean mutually exclusive global modes.

## 3. Modify a workspace

A valid direction is:

~~~text
cli
 | \
 |  \
 v   v
storage
 |
 v
domain
~~~

Domain remains reusable and dependency-light.

## 4. Build optional JSON support

A conceptual storage manifest is:

~~~toml
[features]
default = []
json = ["dep:serde", "dep:serde_json"]

[dependencies]
domain = { path = "../domain" }
serde = { workspace = true, optional = true }
serde_json = { workspace = true, optional = true }
~~~

The CLI can request:

~~~toml
storage = { path = "../storage", features = ["json"] }
~~~

The main architectural check is that domain remains independent from JSON representation details.

A different implementation is acceptable if the dependency direction and feature behavior satisfy the requirements.
