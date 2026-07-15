# Exercise: Validate imported settings

Create a Cargo project and add `serde` with `derive` plus `serde_json`.

1. Define `RawSettings { username: String, refresh_seconds: u64 }` with `Deserialize` and `deny_unknown_fields`.
2. Define `Settings` with the same fields kept private.
3. Implement `TryFrom<RawSettings>` for `Settings`.
4. Reject a blank username and refresh values outside 5 through 3600.
5. Parse one valid JSON string, validate it, and print its fields through accessor methods.
