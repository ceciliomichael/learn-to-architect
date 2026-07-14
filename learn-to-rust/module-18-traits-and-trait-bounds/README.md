# Module 18: Traits and Trait Bounds

A trait names behavior that different types can provide. It is similar to a promise: a type implementing `Summary` must supply the required methods.

```rust
trait Summary {
    fn title(&self) -> &str;

    fn summary(&self) -> String {
        format!("Item: {}", self.title())
    }
}

struct Article {
    title: String,
}

impl Summary for Article {
    fn title(&self) -> &str {
        &self.title
    }
}
```

A bound says what generic code needs:

```rust
trait Summary {
    fn summary(&self) -> String;
}

fn print_summary(item: &impl Summary) {
    println!("{}", item.summary());
}
```

The longer `fn print_summary<T: Summary>(item: &T)` form is useful when `T` appears more than once. A `where` clause keeps several bounds readable.

Traits can contain default methods, associated functions, and associated types. Associated types are useful when an implementation has one natural related type. Rust's orphan rule allows a trait implementation when your crate owns the trait or the type. This prevents unrelated crates from creating conflicting implementations.

`impl Trait` in a return position hides one concrete return type. It does not let different branches return unrelated types. Trait objects for that need appear in Module 23.

## Design guidance

- Keep a trait focused on one useful capability.
- Require only the bounds the function actually uses.
- Use default methods when the default is correct for most implementors.
- Prefer concrete types when callers do not benefit from substitution.

Continue to [Module 19](../module-19-lifetimes/README.md).
