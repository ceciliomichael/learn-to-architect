# Module 35: Documentation, API Design, and Compatibility

Public API includes more than function signatures. Behavior, errors, panic conditions, thread guarantees, feature names, and serialized formats may all become promises callers depend on.

Use `///` for item documentation and `//!` for crate or module documentation. Rustdoc runs fenced Rust examples as tests.

```rust
/// Doubles a value.
///
/// # Examples
///
/// ```
/// assert_eq!(course_core::double(4), 8);
/// ```
pub fn double(value: i32) -> i32 {
    value * 2
}
```

Document what callers need: units, valid ranges, ownership effects, errors, panic cases, and a short working example. Do not merely repeat the function name.

Keep fields private when callers should not construct invalid states. Return specific useful types and require only necessary trait bounds. Once a public enum is intended to accept future variants, `#[non_exhaustive]` can require external matches to include a fallback.

Semantic versioning communicates compatibility intent: breaking public changes require a new major version after 1.0. Before 1.0, Cargo treats the leftmost nonzero component as the compatibility boundary. Mark an old API with a specific message such as `#[deprecated(note = "use new_name instead")]`, provide a migration path, and remove it only in an allowed breaking release.

Run `cargo doc --no-deps` and read the result as a new user would.

Continue to [Module 36](../36-measure-and-improve-performance/README.md).
