# Module 11: Optional Values with Option

## What you will learn

You will represent presence or absence without null references or sentinel values.

`Option<T>` is `Some(T)` or `None`:

```rust
fn find_label(id: u32) -> Option<String> {
    match id {
        1 => Some(String::from("active")),
        _ => None,
    }
}
```

Match directly before using combinators. `as_ref` borrows contained data. `map` transforms a present value. `and_then` chains an operation already returning Option. `unwrap_or` supplies a cheap default; `unwrap_or_else` computes one lazily.

Ask whether you want to keep ownership before choosing a method. Matching `name` moves a contained `String`, while matching `&name` borrows it. `as_ref` changes `Option<String>` into `Option<&String>`, and `as_deref` commonly changes it into `Option<&str>`. These forms let the original option remain usable.

Choose a default only when it is truly valid domain behavior. Showing `"Unknown"` can make sense in a display, but silently replacing a missing price with zero would change the meaning of the data. A match is often the clearest form when `Some` and `None` need different actions.

Avoid `unwrap` for expected absence at external boundaries. It panics and removes useful recovery. `expect` can document a proven internal invariant in carefully controlled code, but proof should be clear.

Use `Option` when absence is normal. The next module introduces a different return type for operations that need to explain why they failed.

## Check your understanding

You are ready when you can handle both variants without inventing a sentinel.
