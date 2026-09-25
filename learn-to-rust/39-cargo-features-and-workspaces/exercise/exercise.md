# Exercises: Module 39

Work in a real local workspace.

## 1. Trace the graph

Given:

~~~text
cli -> storage -> domain
cli ----------> domain
~~~

Answer:

1. Which package can know about the command-line parser?
2. Which package should contain business rules if those rules must also be reusable by another application?
3. Can domain call storage directly under this graph?

Explain every answer using dependency direction.

## 2. Repair a feature design

Start with this conceptual feature table:

~~~toml
[features]
sqlite = []
postgres = []
~~~

The package assumes exactly one database feature is enabled.

Explain why that can be fragile.

Redesign the choice using one of these approaches:

- runtime configuration behind a common application interface;
- separate adapter packages;
- another design you can justify.

Do not solve it only by adding compile errors for every invalid combination unless the package contract truly requires compile-time exclusivity.

## 3. Modify a workspace

Create:

~~~text
workspace/
  crates/
    domain/
    storage/
    cli/
~~~

Make:

~~~text
storage -> domain
cli -> storage
cli -> domain
~~~

Then run:

~~~text
cargo check --workspace
cargo test --workspace
~~~

Add at least one unit test in domain.

## 4. Build optional JSON support

In storage, add Serde JSON support behind a feature named json.

Requirements:

- storage must compile with no default features;
- json activates only the JSON-related dependency;
- domain must not gain a serde_json dependency;
- the CLI must explicitly enable storage's json feature if it uses JSON storage.

Verify with:

~~~text
cargo check -p storage --no-default-features
cargo check -p storage --features json
cargo tree -p storage
~~~

## Completion standard

Write a short ARCHITECTURE.md containing:

- package responsibilities;
- dependency arrows;
- supported feature combinations;
- why each external dependency belongs in its package.
