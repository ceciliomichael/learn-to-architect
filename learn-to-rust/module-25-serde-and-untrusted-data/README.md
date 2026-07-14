# Module 25: Serde and Untrusted Data

Serde converts Rust data structures to and from formats such as JSON. Add dependencies with Cargo so it selects current compatible releases:

```text
cargo add serde --features derive
cargo add serde_json
```

```rust
use serde::{Deserialize, Serialize};

#[derive(Debug, Serialize, Deserialize)]
#[serde(deny_unknown_fields)]
struct RawAccount {
    name: String,
    age: u8,
}
```

Deserialization proves that data matches the serialized shape. It does not prove that a name is acceptable, an age is allowed, or a path is safe. Keep a raw input type at the boundary, validate it, and then create the domain type used by the rest of the program.

`deny_unknown_fields` catches misspelled or unexpected fields when strict input is appropriate. Other systems need forward compatibility and deliberately ignore new fields. Choose the policy as part of the input contract rather than by habit.

Always limit request or file size before deserializing untrusted data. Avoid deeply nested or enormous inputs, return useful errors without exposing secrets, and never deserialize into a type that immediately performs privileged actions.

The Rust Playground does not support adding arbitrary dependencies through a `Cargo.toml`, so use a local Cargo project for this module.

Continue to [Module 26](../module-26-threads-and-scoped-threads/README.md).
