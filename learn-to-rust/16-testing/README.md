# Module 16: Test Rust Code

## What you will learn

You will write isolated unit, integration, error, and documentation tests with Cargo.

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn adds_values() {
        assert_eq!(add(2, 3), 5);
    }
}
```

`cargo test` compiles and runs tests. Unit tests live near private code. Integration tests under `tests/` use only the library's public API. A test can return `Result<(), E>` and use `?`.

Name a test after one rule and arrange it in three visible parts: create the input, perform the action, and check the result. Include ordinary values, meaningful boundaries, and expected errors. A test that only repeats the implementation does not add much confidence.

Use `assert_eq`, `assert_ne`, and `matches!` with useful context. `#[should_panic]` is for a documented panic contract, not ordinary error results. Documentation examples run as tests by default.

Tests run in parallel by default and their order is not promised. Shared files, fixed ports, global environment changes, and one common database can make tests interfere with each other. Give each test independent state or synchronize the boundary deliberately.

Give each test fresh state. Use unique temporary directories from a reviewed helper or standard temporary path strategy and clean them reliably. Avoid public networks, real clocks, and shared environment mutation without isolation.

A failing test should help locate the broken rule. Keep assertions focused and include relevant values in failure messages. Coverage can reveal code that never ran, but a covered line is not necessarily checked correctly.

## Check your understanding

You are ready when every failure names a rule and tests remain independent of order.
